Reset forms are often less well protected than login ones. Therefore, they very often leak information about a valid or invalid username. An application that replies with a "You should receive a message shortly" when a valid username has been found and "Username unknown, check your data" for an invalid entry leaks the presence of registered users.