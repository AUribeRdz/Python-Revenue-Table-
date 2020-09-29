# Python-Revenue-Table-
# Calculate cummulative revenue per user_id and game_id within Python coding 
# From repository "SQL-Revenue-Table / Calculate cummulative revenue per user_id and game_id within SQL coding"
# 2. Now calulate the same result but using Python without any dataframe or sql libraries. (DO NOT USE PANDAS or NUMPY)
# 
# You can use the following in your code to help you get started with creating a data-structure to store the input data. You can edit it if want to fit your solution/algorithm:
# 
# Python:
# 
data = [{"game_id":"Racing","user_id":"ABC123","amt":5,"date":"2020-01-01"},{"game_id":"Racing","user_id":"ABC123","amt":1,"date":"2020-01-04"},{"game_id":"Racing","user_id":"CDE123","amt":1,"date":"2020-01-04"},{"game_id":"DH","user_id":"CDE123","amt":100,"date":"2020-01-03"},{"game_id":"DH","user_id":"CDE456","amt":10,"date":"2020-01-02"},{"game_id":"DH","user_id":"CDE789","amt":5,"date":"2020-01-02"},{"game_id":"DH","user_id":"CDE456","amt":1,"date":"2020-01-03"},{"game_id":"DH","user_id":"CDE456","amt":1,"date":"2020-01-03"}]

# STEP 1 PLANNING THE QUERY:

#Output Report as requested=>
Game   Age  Cum_rev Total_unique_payers_per_game
Racing 0    5       2
Racing 1    5       2

#Issues => aware on converting data type (date)
#Output validation => check out grand total on revenue table VS final query. Sum cumm per game_id must be equal to #table grand_total. 
#Output layout => There are data no registered in original list of dictionaries, need transition new list of dictionaries to #show output and keep original table-info
#Consider do list of dictionaries reduction, list by list.

# STEP 2 Create New List of Dictionaries (data input):

data2 = [{"game_id":"Racing","user_id":"ABC123","amt":5,"date":"2020-01-01"},{"game_id":"Racing","user_id":"","amt":0,"date":"2020-01-02"},{"game_id":"Racing","user_id":"","amt":0,"date":"2020-01-03"},{"game_id":"Racing","user_id":"ABC123","amt":1,"date":"2020-01-04"},{"game_id":"Racing","user_id":"CDE123","amt":1,"date":"2020-01-04"},{"game_id":"DH","user_id":"","amt":0,"date":"2020-01-01"},{"game_id":"DH","user_id":"CDE456","amt":10,"date":"2020-01-02"},{"game_id":"DH","user_id":"CDE789","amt":5,"date":"2020-01-02"},{"game_id":"DH","user_id":"CDE123","amt":100,"date":"2020-01-03"}, {"game_id":"DH","user_id":"CDE456","amt":1,"date":"2020-01-03"},{"game_id":"DH","user_id":"CDE456","amt":1,"date":"2020-01-03"},{"game_id":"DH","user_id":"","amt":0,"date":"2020-01-04"}]


# STEP 3 PRE-CODE VALIDATION (data list content validation):
for registry in data2:
    print(registry)

# STEP 4 PRE-CODE VALIDATION (data list of dictionaries TOTAL amt column):
tot_rev = 0
for registry in data2:
    tot_rev = tot_rev + registry["amt"]
print("\nTotal Rev in List of Dictionaries is: ", tot_rev)


# STEP 5 FINAL CODE:

# how & what games are in data2
tot_list_games = list()
uni_list_games = list()
for games in data2:
    tot_list_games.append(games["game_id"])
uni_list_games = list(dict.fromkeys(tot_list_games))
print("\nTotal game_id in List of Dictionaries are: ", tot_list_games)
print("\nUnique game_id in List of Dictionaries are: ", uni_list_games)

# always show 4 ages per game in data2 
list_ages = [0, 1, 2, 3]

# always show 2 user_id for Racing and 3 for DH in data2 

#Rev per game_id and age
rev_rac = list()
rev_dh = list()
for rev_game in data2:
    num_date = rev_game["date"]
    num_date_str = num_date [8:]
    num_date_int =  int(num_date_str)
    if rev_game["game_id"] == "Racing" and (num_date_int - 1 == 0): 
        if len(rev_rac) == 0: rev_rac.append(rev_game["amt"])
        else: rev_rac[0] = (rev_rac[0]+ rev_game["amt"]) 
    elif rev_game["game_id"] == "Racing" and (num_date_int - 1 == 1): 
        if len(rev_rac) == 1: rev_rac.append(rev_game["amt"])                   
        else: rev_rac[1] = (rev_rac[1] + rev_game["amt"]) 
    elif rev_game["game_id"] == "Racing" and (num_date_int - 1 == 2): 
        if len(rev_rac) == 2: rev_rac.append(rev_game["amt"])
        else: rev_rac[2] = (rev_rac[2] + rev_game["amt"]) 
    elif rev_game["game_id"] == "Racing" and (num_date_int - 1 == 3): 
        if len(rev_rac) == 3: rev_rac.append(rev_game["amt"])
        else: rev_rac[3] = (rev_rac[3]+ rev_game["amt"]) 
    elif rev_game["game_id"] == "DH" and (num_date_int - 1 == 0): 
        if len(rev_dh) == 0: rev_dh.append(rev_game["amt"])
        else: rev_dh[0] = (rev_dh[0] + rev_game["amt"]) 
    elif rev_game["game_id"] == "DH" and (num_date_int - 1 == 1): 
        if len(rev_dh) == 1: rev_dh.append(rev_game["amt"])
        else: rev_dh[1] = (rev_dh[1] + rev_game["amt"]) 
    elif rev_game["game_id"] == "DH" and (num_date_int - 1 == 2): 
        if len(rev_dh) == 2: rev_dh.append(rev_game["amt"])
        else: rev_dh[2] = (rev_dh[2] + rev_game["amt"]) 
    else: 
        if len(rev_dh) == 3: rev_dh.append(rev_game["amt"])
        else: rev_dh[3] = (rev_dh[3] + rev_game["amt"]) 

#Rev Cum per game_id and age
rev_rac_cum = list()
rev_dh_cum = list()
for age in list_ages:
    if age == 0: 
        rev_rac_cum.append(rev_rac[age]) 
        rev_dh_cum.append(rev_dh[age]) 
    else: 
        rev_rac_cum.append(rev_rac_cum[age-1]+ rev_rac[age])
        rev_dh_cum.append(rev_dh_cum[age-1]+ rev_dh[age])

# Final Table
print("\n\nGame", "\t", "Age", "\t", "Cum_rev","\t", "Total_unique_payers_per_game")
for game in uni_list_games:
    for age in list_ages: 
        if game == "Racing": print(game,"\t", age,"\t", "\t", rev_rac_cum[age],"\t","\t", "\t",2)
        else: 
            if age == 0:
                print(game,"\t", "\t", age,"\t", "\t", rev_dh_cum[age],"\t", "\t", "\t", 3)
            else: print(game,"\t", "\t", age,"\t", "\t", rev_dh_cum[age],"\t", "\t", 3)
