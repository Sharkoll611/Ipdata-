#!/usr/bin/python3

# Name          : ipdata
# Writer(s)     : sharkolle611
# Description   : ipdata is a simple IP Tracker using Python.

import os
import urllib.request
import json
import colorama

colorama.init(autoreset=True)

os.system("clear")
print(colorama.Fore.GREEN + '''
###     ### ### ##
###     ### ### ##
        ###      #
###     ###      #
###     ### ### ##
###     ### ### ##
###     ###
###     ###   DATA

Welcome!
''')
print("\r")

while True:
    ip = input(colorama.Fore.GREEN + "What is your target IP: ")
    url = f"https://api.ipdata.co/{ip}?api-key=e7045c876f948ae92ce55787cf1b9a75ce5980c707fdc397e8e2606a"  # Replace 'test' with your actual API key

    try:
        with urllib.request.urlopen(url) as response:
            data = response.read()
            values = json.loads(data)

        print("------------------------------------")
        print("\r")
        print(f" IP           :  {values.get('ip', 'N/A')}")
        print(f" City         :  {values.get('city', 'N/A')}")
        print(f" Region       :  {values.get('region', 'N/A')}")
        print(f" Country      :  {values.get('country_name', 'N/A')}")
        print(f" Continent    :  {values.get('continent_name', 'N/A')}")
        print(f" Time Zone    :  {values.get('time_zone', {}).get('name', 'N/A')}")
        print(f" Currency     :  {values.get('currency', {}).get('name', 'N/A')}")
        print(f" Calling Code :  +{values.get('calling_code', 'N/A')}")
        print(f" Organisation :  {values.get('organisation', 'N/A')}")
        print(f" ASN          :  {values.get('asn', {}).get('asn', 'N/A')}")
        print("\r")
        break
    except urllib.error.URLError as e:
        print(colorama.Fore.RED + f"Error: Unable to fetch data. {e}")
        break
    except json.JSONDecodeError:
        print(colorama.Fore.RED + "Error: Unable to parse JSON response.")
        break
