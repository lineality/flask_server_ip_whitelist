# flask_server_ip_whitelist
screen user ip against a whitelist

```
whitelist_dictionary_ip_game = {
"NAME_OF_GAME": """place_name_0.0.0.0""",
}

# helper function
def get_user_ip():
    """
    Flask app get ip of user.
    """
    if request.headers.getlist("X-Forwarded-For"):
        user_ip = request.headers.getlist("X-Forwarded-For")[0]
        print("\nuser ip from proxy port forwarding list\n")

    else:
        user_ip = request.remote_addr
        # Terminal Print
        print("\nNormal IP, no proxy or forwarding.\n")

    user_ip = str(user_ip)
    user_ip = user_ip.replace(' ','')

    print(f"user user_ip:\n'{user_ip}'", )

    return user_ip

# helper function
def check_ip_whitelist(game_name, user_ip):
    """
    Also requires another helper function and lookup dict (or other lookup): 
        - get_user_ip()
        - whitelist_dictionary_ip_game = {}
        
    Example Use:
    
    # set inputs:
    game_name = "NAME_OF_GAME"
    the_user_is = get_user_ip()
    
    # run the check:
    boolean_ip_whitelist_check = check_ip_whitelist( game_name, the_user_is)
    
    print(boolean_ip_whitelist_check)
    """
    
    output = False

    try:
        if user_ip in whitelist_dictionary_ip_game[game_name]:
            output = True

    except:
        # default to false, if for whatever reason check does not work
        pass

    return output
```
