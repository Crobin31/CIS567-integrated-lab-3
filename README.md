def read_customer_data(filename):
    """Read and return data from filename as a list of lists (name, state, debt)"""
    names = []
    states = []
    debts = []

    with open(filename) as f:
        rows = f.readlines()
    for row in rows:
        row = row.split(',')
        names.append(row[0])
        states.append(row[1])
        debts.append(float(row[2].strip()))
    return names, states, debts

# Main portion of the program
if __name__ == '__main__':
    # number of rows to consider
    num_customers = int(input())

    names, states, debts = read_customer_data("CustomerData.csv")

    # Type your code here.
    debt_limit = int(input())
    search_phrase = input()
    state_abbrev = input()

    max_debt = -1.0
    highest_debt_name = ""
    phrase_count = 0
    debt_over_limit = 0
    debt_free = 0

    for i in range(num_customers):
        if debts[i] > max_debt:
            max_debt = debts[i]
            highest_debt_name = names[i]
        
        if names[i].startswith(search_phrase):
            phrase_count += 1
            
        if debts[i] > debt_limit:
            debt_over_limit += 1
        if debts[i] == 0:
            debt_free += 1

    print("U.S. Report")
    print(f"Customers: {num_customers}")
    print(f"Highest debt: {highest_debt_name}")
    print(f"Customer names that start with \"{search_phrase}\": {phrase_count}")
    print(f"Customers with debt over ${debt_limit}: {debt_over_limit}")
    print(f"Customers debt free: {debt_free}")

    state_max_debt = -1.0
    state_highest_name = ""
    state_phrase_count = 0
    state_debt_over = 0
    state_debt_free = 0
    state_total_customers = 0

    for i in range(num_customers):
        if states[i] == state_abbrev:
            state_total_customers += 1
            
            if debts[i] > state_max_debt:
                state_max_debt = debts[i]
                state_highest_name = names[i]
            
            if names[i].startswith(search_phrase):
                state_phrase_count += 1
                
            if debts[i] > debt_limit:
                state_debt_over += 1
            
            if debts[i] == 0:
                state_debt_free += 1

    print(f"\n{state_abbrev} Report")
    print(f"Customers: {state_total_customers}")
    print(f"Highest debt: {state_highest_name}")
    print(f"Customer names that start with \"{search_phrase}\": {state_phrase_count}")
    print(f"Customers with debt over ${debt_limit}: {state_debt_over}")
    print(f"Customers debt free: {state_debt_free}")
