##############################################################################################
# Presenters
# Dean Osher Friedlender
# Mathias Vaserman

# The program's variables [list & dictionaries]
only_user = []
only_user_unique = []
only_movie = []
movies_to_watch = {}
ls_movies = []
dic_user = {}
# a given dictionary of movies and ratings
Watched_movies = {"matrix": 9.0, "Thor love and thunder": 8.3,
                  "green book": 8.3, "her": 8.1, "the evil dead": 7.8,
                  "forrest gump": 9.2, "life aquatic": 9.5,
                  "life of bryan": 7.9, "first blood": 8.9}
# A name input that appends to an empty list called "only_user"
# The input will be remembered till the user will quit or change user
user_name = str(input('Please enter your name: '))
only_user.append(user_name)
count = 0
rounds = 0
# The start of the loop where the user is asked another question with 3 inputs
# (enter movie name, choose quitting, choose changing a user)
while rounds < 1:
    movie = str(input("Enter a name of a movie you've watched recently, "
                      "enter cu to change user or press q to quit.: ")).casefold()
    # The 'q' option allows the user to end the loop and quit the program
    # Presents the summary of the program from start to end
    if movie.casefold() == "q":
        rounds = 1
        # Check if one user was entered and no movies were added
        if len(dic_user.keys()) == 1 and len(only_movie) == 0:
            print(f"Well we had one user today going by the name {only_user_unique} and "
                  "nothing was added to movies_to_watch")
        # Check if one user was entered and at least 1 movie were added
        if len(dic_user.keys()) == 1 and len(only_movie) > 0:
            print(f"Well we had one user today going by the name {only_user_unique} and "
                  f"these were added to movies_to_watch")
            print(dic_user)
        # Check if more than one user was entered and no movies were added
        if len(dic_user.keys()) > 1 and len(only_movie) == 0:
            print(f"Well we had {len(only_user_unique)} users today going by the names: {only_user_unique} and "
                  "nothing was added to movies_to_watch")
        # Check if more than user was entered and at least 1 movie were added
        if len(dic_user.keys()) > 1 and len(only_movie) > 0:
            print(f"Well we had {len(only_user_unique)} users today going by the names: {only_user_unique} and "
                  f"these were added to movies_to_watch")
            print(dic_user)
    # The 'cu' option allows the user to change user and restart the program
    elif movie.casefold() == "cu":
        # The 'cu' option is an input that will be remembered until the user will quit or change user
        # The user name will be stored in the only_user list
        user_name = str(input('Please enter your name: '))
        only_user.append(user_name)
        only_user_unique = []
        # Check for unique user_name in the list only_user
        # Copy the unique variable to the new list [only_user_unique]
        for user_name in only_user:
            if user_name not in only_user_unique:
                only_user_unique.append(user_name)
                rounds = 0
    # The user wrote a movie name that's in the Watched_movies dictionary and has to rate it from 1 to 10
    # The input [rating_prime] will be remembered till the user will start the loop again
    # The input will be saved in the movies_to_watch dictionary
    elif movie.casefold() in Watched_movies:
        print(f"I've watched that movie as well i rate it {Watched_movies[movie]}")
        rating_prime = float(input("what's your rating between 1 and 10? "))
        if abs(rating_prime - Watched_movies[movie]) <= 2:
            print("wow we have similar taste")
        else:
            print('well i guess we will agree to disagree :)')
    # The user wrote a movie name that is not in the Watched_movies and has to rate it from 1 to 10
    # The input [rating] will be remembered till the user will start the loop again
    elif movie not in Watched_movies:
        rating = float(input("I haven't watched that one yet, "
                             "how would you rate it on a scale from 1 to 10? "))
        # check if the input is grater or equal to 7
        if rating >= 7:
            count += 1
            # The new movie will be stored in separate list to be counted at the summation of the loop
            only_movie.extend(movie)
            # The new movie and his assigned rating will be saved in the movies_to_watch dictionary
            movies_to_watch = {movie: rating}
            # The dictionary movies_to_watch will be converted to a list ls_movies
            ls_movies.append(list([movies_to_watch]))
            # The user_name and the list ls_movies will be converted to a key and a value in the dictionary dic_user
            # After the user enter the required details the next if program will check if there is an exiting user
            # If there is the program will add the new details to the exiting, if not it will crate a new key and value
            if user_name in dic_user.keys():
                dic_user[user_name] = dic_user[user_name] + ls_movies[count - 1]
            else:
                dic_user[user_name] = ls_movies[count - 1]
            print(f"The movie {movie} was added to movies_to_watch list")
        else:
            print("Well my minimum is 7 so guess we wont be watching this one soon :)")

##############################################################################################
