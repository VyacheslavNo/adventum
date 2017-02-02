# adventum
Test task for adventum. Big Data Developer/Analyst. Google Analytics:

import pandas as pd
import numpy as np
from pyparsing import *

data = pd.read_csv('adventum2.csv', skiprows=7, header=None, error_bad_lines=False, warn_bad_lines=False)
ccc = {}

N_string = 6

iii = 0
while iii < len(data):
########################################################
    s = data.loc[iii].values[0]
    # парсим первый столбец
    source = Word(alphas + '.' + '(' + ')')
    channel = Word(alphas + '(' + ')')
    viraj = source + '/' + channel
    fullviraj = viraj + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj) + Optional('>' + viraj)
    b = fullviraj.parseString(s).asList()
    bb = []
    i = 0
    while i < (len(b)+1)/2: # Удалим ненеужные элементы из строки
        bb.append(b[i*2])
        i = i + 1
    #print(bb)
    cpm = 'cpm'
    cpc = 'cpc'
    referral = 'referral'
    c = {}
    i = 0
    kolvo_platnix = 0
    while i < len(bb): # определяем сколько в строке платных элементов и заполняем словарь
        if bb[i]==cpm:
            st = bb[i-1] + '/' + bb[i]
            c[st] = c.setdefault(st, 0) + 1
            kolvo_platnix = kolvo_platnix +1
        elif bb[i]==cpc:
            st = bb[i-1] + '/' + bb[i]
            c[st] = c.setdefault(st, 0) + 1
            kolvo_platnix = kolvo_platnix +1
        elif bb[i]==referral:
            st = bb[i-1] + '/' + bb[i]
            c[st] = c.setdefault(st, 0) + 1
            kolvo_platnix = kolvo_platnix + 1
        i = i + 1
    #print(c)
    #парсим бабло
    string_price = data.loc[iii].values[2]
    number = Word(nums)
    line = Optional(number + '\xa0') + Optional(number + '\xa0') + Optional(number + '\xa0') + Optional(number + '\xa0') + number + ',' + number
    prices = line.parseString(string_price)
    i = 0
    prices_str = ''
    while i < ((len(prices))-1)/2:
        prices_str = prices_str + prices[i*2]
        i = i + 1
    prices_str_float = float(prices_str) +  float(prices[i*2])/100
    #print(string_price)
    #print(prices_str_float)
    if kolvo_platnix != 0:
        price_onepart = prices_str_float/kolvo_platnix
    else:
        price_onepart = 0
    keyss = c.keys()
    #print(keyss)
    for f in keyss:
        c[f] = c[f]*price_onepart
        if c[f] != 0:
            ccc[f] = ccc.setdefault(f, 0) + c[f]
    #print(c)
    iii = iii + 1
##############################################################

#print(ccc)
l = lambda x: x[1]
ccc = sorted(ccc.items(), key=l, reverse=True)
print(ccc)





#while i < len(c):
    
#countRA = np.array([[1, 2, 3], [4, 5, 6]])
#print(countRA[0][1])
#print(bb.count(cpm), bb.count(cpc), bb.count(referral))



