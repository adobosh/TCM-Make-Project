# TCM-Make-Project

I am making my final project and I'm really excited about it.

Coronavirus API, symptom check and testing center


import requests, json, pprint

def intro(): #Makes the program more user friendly by giving an intro and asking for their name.

    print('Hi! Welcome to COVID-19 tracker. During these tough times, we want to provide you with the most up to date information.')
    print ('Please introduce yourself, what is your name?')
    myName = input()


def PickACountry():

    print('Please enter a country you would like to receive information regarding COVID-19.') #United States = US
    stats = input()
    URL = f'https://thevirustracker.com/free-api?countryTimeline={stats}'
    response = requests.get(URL)
    response.raise_for_status
    return response

def getinfo(jsonData):
    coronaList = []

intro()
response = PickACountry()
jsonData = json.loads(response.text)
pprint.pprint(jsonData)



------

import requests, json, pprint, datetime

date = ''

def intro(): #Makes the program more user friendly by giving an intro and asking for their name.

     print('Hi! Welcome to COVID-19 tracker. During these tough times, we want to provide you with the most up to date information.')
     print ('Please introduce yourself, what is your name?')
     myName = input()

def PickACountry():

     print('Please enter a country you would like to receive information regarding COVID-19.') #United States = US
     stats = input()
     URL = f'https://thevirustracker.com/free-api?countryTimeline={stats}'
     response = requests.get(URL)
     response.raise_for_status
     return response

def PickADate():
    global date
    print('This COVID-19 tracker is updated at the end of each day and thus the most recent information is for yesterdays date.')
    print('Please enter any date from 1/22/20 until yesterdays date that you would like to receive information about.')
    print('Using this format: X/XX/XX.')
    date = str(input())

def getInfo(jsonData):

    coronaList = []
    coronaList.append(jsonData['countrytimelinedata'][0]['info']['title'])
    coronaList.append(jsonData['countrytimelinedata'][0]['info']['source'])
    coronaList.append(jsonData['timelineitems'][0][date])

    for x in range(len(coronaList)):
        print(coronaList[x])

intro()
response = PickACountry()
PickADate()
jsonData = json.loads(response.text)
getInfo(jsonData)
#pprint.pprint(jsonData)
