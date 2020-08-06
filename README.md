# DataCleaningAndPandas

#Cleaning File
flist = open(r"C:\Users\Rajat\Downloads\Ecommerce Purchases.txt").readlines()
outF = open(r"C:\Users\Rajat\Downloads\myOutFile.txt", "w")
i = 0
for s in flist:
    if i%2 != 0:
        outF.write(s.rstrip('\n'))
        i+=1
    else:
        outF.write(s)
        i+=1
outF.close()
#Importing File
import pandas as pd
df = pd.read_csv(r"C:\Users\Rajat\Downloads\myOutFile.txt", sep = "," )
2
df.head(2)
df.shape
df.info()
#Someone made a purchase that came from Lot: "90 WT" ,what was the Purchase Price for this transaction?
df[df["Lot"] == "90 WT"]
df[df["Lot"] == "90 WT"]["Purchase Price"]
#What is the email of the person with the following Credit Card Number: 4926535242672853
df[df["Credit Card"] == 4926535242672853]
df[df["Credit Card"] == 4926535242672853]
df[df["Credit Card"] == 4926535242672853]["Email"]
#How many people have American Express as their Credit Card Provider and made a purchase above $95 ?
df[(df['Purchase Price'] > 95) & (df["CC Provider"] == "American Express")]['Email'].count()
#How many people have a credit card that expires in 2025?
df[df['CC Exp Date'].str[-2:] == '25']['Email'].count()
#What are the top 5 most popular email providers/hosts (e.g. gmail.com, yahoo.com, etc...)
new = df["Email"].str.split("@", n = 1, expand = True)
new
df["Host"] = new[1]
df.groupby(['Host']).count().sort_values(by=['Address'], ascending = False)[["Language"]].head()
