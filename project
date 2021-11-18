test

import requests
import json
import pprint
import matplotlib.pyplot as plt
import numpy as np

#Finds data for a user and server.
def requestSummonerData(server, summonerName, APIKey):
    #URL = "https://" + server + ".api.pvp.net/api/lol/" + server + "/v4/summoner/by-name/" + summonerName + "?api_key=" + APIKey
    APIKey = "RGAPI-e16b87f1-95f5-4927-ae19-3e9baa0c6649"
    server = "na1"
    summonerName = "Jamishio" #This will have to be removed
    
    URL = "https://" + server + ".api.riotgames.com/lol/summoner/v4/summoners/by-name/" + summonerName + "?api_key=" + APIKey
    
    print(URL)
    print("")
    #requests.get is a function given to us by our import "requests". It basically goes to the URL we made and gives us back a JSON.
    response = requests.get(URL)
    #Here I return the JSON we just got.
    return response.json()

#Gets matches played by the user inputted earlier
def matchList(accountId, APIKey):

    URL = "https://na1.api.riotgames.com/lol/match/v4/matchlists/by-account/" + accountId + "?api_key="  + APIKey
    #APIKey = "RGAPI-bb2d9042-4ec2-4cc1-a212-3ba3e24a64ad"
    response = requests.get(URL)
    return response.json()

#Gets information for a specific match
def matchData(gameids, APIKey):

    killsList = []
    firstBloodKillList = []
    minionKillsList = []
    winsList = []
    for gameid in gameids[:199]: #Loads number of gameids

        URL = "https://na1.api.riotgames.com/lol/match/v4/matches/" + str(gameid) + "?api_key=" + APIKey
        response = requests.get(URL)
        response = response.json()
        print("Printing...")
        
        try:
            kills = response["participants"][0]["stats"]["kills"] #Prints out data for the first user.
            firstBloodKill = response["participants"][0]["stats"]["firstBloodKill"]
            minionsKills = response["participants"][0]["stats"]["totalMinionsKilled"]
            wins = response["participants"][0]["stats"]["win"]
            killsList.append(kills)
            firstBloodKillList.append(firstBloodKill)
            minionKillsList.append(minionsKills)
            winsList.append(wins)
        except:
            pass #Removes any data with missing information that could ruin our data.
    
    #print(kills, firstBloodKill, minionsKills, wins) 
    #print(killsList, firstBloodKillList, minionKillsList, winsList)
    #return killsList, firstBloodKillList, minionKillsList, winsList
    return winsList

#Tests the data without having to deal with rate limits.
def testing(gameids, APIKey):
    #count = 0
    killsList = []
    firstBloodKillList = []
    minionKillsList = []
    winsList = []
    for gameid in gameids[:5]: #Loads 1 gameids
        #count += 1
        URL = "https://na1.api.riotgames.com/lol/match/v4/matches/" + str(gameid) + "?api_key=" + APIKey
        response = requests.get(URL)
        response = response.json()
           
        try:
            kills = response["participants"][0]["stats"]["kills"] #Prints out data for the first user.
            firstBloodKill = response["participants"][0]["stats"]["firstBloodKill"]
            minionsKills = response["participants"][0]["stats"]["totalMinionsKilled"]
            wins = response["participants"][0]["stats"]["win"]
            killsList.append(kills)
            firstBloodKillList.append(firstBloodKill)
            minionKillsList.append(minionsKills)
            winsList.append(wins)
        except:
            pass #Removes any data with missing information.    
        
        print("Kills: ", kills, "FirstBlood: ", firstBloodKill, "CS:",  minionsKills,"Wins: ", wins) 
        return killsList, firstBloodKillList, minionKillsList, wins
    
#Graphs all of the data.
def graphs(kills, firstBloodKill, minionsKills, wins):
    numberOfGames = len(kills)
    games = np.arange(numberOfGames)
    #print(games)
    #plt.subplot(221)
    
    plt.scatter(games, kills) #Scatter plot for number of kills.
    plt.title("Number of Kills for Each Game")
    plt.xlabel('Number of games')
    plt.ylabel('Number of kills')
    #plt.legend()
    
    #plt.subplot(222)
    
#Bar graph that shows number of wins and losses. 
def WinsBarGraph(wins, winsList):
    numberOfGames = len(winsList)
    print("wins", winsList)
    games = np.arange(numberOfGames)
    plt.bar(games, wins)
    plt.title("Win Ratio")
    plt.xlabel("Number of games")
    plt.ylabel("Wins")
    plt.legend()

#Bar graph that shows number of first bloods. 
def firstBloodBarGraph(kills, firstBloodKill, minionsKills, wins):
    numberOfGames = len(firstBloodKill)
    games = np.arange(numberOfGames)
    plt.bar(games, firstBloodKill)
    plt.title("First Bloods")
    plt.xlabel("Number of games")
    plt.ylabel("First Bloods")
    
#Scatter plot that shows number of minions killed per game. 
def minionsBarGraph(kills, firstBloodKill, minionsKills, wins):
    numberOfGames = len(minionsKills)
    games = np.arange(numberOfGames)
    plt.scatter(games, minionsKills)
    plt.title("Number of Minions Killed")
    plt.xlabel("Number of games")
    plt.ylabel("Minions Killed")
    
def main():
    #Allows users to input their own data.
    print("Please enter a server from this list: NA1, RU, KR, BR1, OC1, JP1, EUN1, EUW1, TR1, LA1, LA2")
    #server = (str)(input('Please enter a server: '))  #Add error handling
    #summonerName = (str)(input('Please enter a summoner name: '))
    #APIKey = (str)(input('Please enter your API key: '))

    #if server != "na1", "RU", "KR", "BR1", "OC1", "JP1", "EUN1", "EUW1", "TR1", "LA1", "LA2":
    #    print("Please enter a valid server.")
        
    #Testing data to make it simpler.
    APIKey = "RGAPI-e16b87f1-95f5-4927-ae19-3e9baa0c6649"
    server = "na1"
    summonerName = "Jamishio"
    
    responseJSON = requestSummonerData(server, summonerName, APIKey)
    #print(responseJSON) #Prints out data for summonerName
    
    accountId = responseJSON["accountId"]
   
    #print(accountId) #Prints out players account ID.

    matches = matchList(accountId, APIKey)
    gameids = [item['gameId']for item in matches['matches']]
    
    #print(gameids) #Prints out game IDs for 100 games.
    #print(matches['matches'][0]['gameId']) #Prints out the first match ID.
    
    #data = matchData(gameids, APIKey)
    kills, firstBloodKill, minionsKills, wins = testing(gameids, APIKey) #Use this line for testing
    winsList = matchData(gameids, APIKey)
    print("winsList: ", winsList)
    #kills, firstBloodKill, minionsKills, wins = matchData(gameids, APIKey) #Use this line for real data.
    graphs(kills, firstBloodKill, minionsKills, wins)
    WinsBarGraph(wins, winsList)
    firstBloodBarGraph(kills, firstBloodKill, minionsKills, wins)
    minionsBarGraph(kills, firstBloodKill, minionsKills, wins)
    #print(data["gameId"]) #Prints gameId (The number in matchData)   
    
    #pprint.pprint(data) #Prints out everything in a better view.
    
    #gameId = matches["gameId"]
    #games = gameId()
    #print(gameId)
    
if __name__ == "__main__":
    main()
