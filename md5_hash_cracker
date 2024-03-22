import re
import os
import requests
import concurrent.futures

# Colors and formatting
end = '\033[0m'
red = '\033[91m'
info = '\033[93m[!]\033[0m'
bad = '\033[91m[-]\033[0m'
bold = '\033[1m'
green = '\033[38;2;0;255;0m'
cwd = os.getcwd()

def alpha(hashvalue, hashtype):
    return False

def beta(hashvalue, hashtype):
    response = requests.get('https://hashtoolkit.com/reverse-hash/?hash=' + hashvalue).text
    match = re.search(r'/generate-hash/\?text=(.*?)"', response)
    if match:
        return match.group(1)
    else:
        return False

def gamma(hashvalue, hashtype):
    # Suppressing the InsecureRequestWarning
    requests.packages.urllib3.disable_warnings(requests.packages.urllib3.exceptions.InsecureRequestWarning)
    
    response = requests.get('https://www.nitrxgen.net/md5db/' + hashvalue, verify=False).text
    if response:
        return response
    else:
        return False

def theta(hashvalue, hashtype):
    response = requests.get('https://md5decrypt.net/Api/api.php?hash=%s&hash_type=%s&email=deanna_abshire@proxymail.eu&code=1152464b80a61728' % (hashvalue, hashtype)).text
    if len(response) != 0:
        return response
    else:
        return False

print ('''\033[1;97m
\033[38;2;200;0;200m███╗░░░███╗██████╗░███████╗  ██╗░░██╗░█████╗░░██████╗██╗░░██╗
\033[38;2;150;50;255m████╗░████║██╔══██╗██╔════╝  ██║░░██║██╔══██╗██╔════╝██║░░██║
\033[38;2;100;100;255m██╔████╔██║██║░░██║██████╗░  ███████║███████║╚█████╗░███████║
\033[38;2;50;150;255m██║╚██╔╝██║██║░░██║╚════██╗  ██╔══██║██╔══██║░╚═══██╗██╔══██║
\033[38;2;0;200;200m██║░╚═╝░██║██████╔╝██████╔╝  ██║░░██║██║░░██║██████╔╝██║░░██║
\033[38;2;0;255;150m╚═╝░░░░░╚═╝╚═════╝░╚═════╝░  ╚═╝░░╚═╝╚═╝░░╚═╝╚═════╝░╚═╝░░╚═╝
\033[38;2;255;136;0m░█████╗░██████╗░░█████╗░░█████╗░██╗░░██╗███████╗██████╗░
\033[38;2;255;136;0m██╔══██╗██╔══██╗██╔══██╗██╔══██╗██║░██╔╝██╔════╝██╔══██╗
\033[38;2;255;136;0m██║░░╚═╝██████╔╝███████║██║░░╚═╝█████═╝░█████╗░░██████╔╝
\033[38;2;255;136;0m██║░░██╗██╔══██╗██╔══██║██║░░██╗██╔═██╗░██╔══╝░░██╔══██╗
\033[38;2;255;136;0m╚█████╔╝██║░░██║██║░░██║╚█████╔╝██║░╚██╗███████╗██║░░██║
\033[38;2;255;136;0m░╚════╝░╚═╝░░╚═╝╚═╝░░╚═╝░╚════╝░╚═╝░░╚═╝╚══════╝╚═╝░░╚═╝%s\033[0m\n''' % red)


md5 = [gamma, alpha, beta, theta]

def crack(hashvalue):
    result = False
    if len(hashvalue) == 32:
        print('%s Hash function : MD5' % info)
        for api in md5:
            r = api(hashvalue, 'md5')
            if r:
                # Check if the result starts with $HEX[
                if r.startswith('$HEX[') and r.endswith(']'):
                    hex_string = r[5:-1]  # Extract the hexadecimal string without the $HEX[]
                    # Convert the hexadecimal string to bytes and decode
                    try:
                        result = bytes.fromhex(hex_string).decode()
                    except ValueError:
                        print('\033[38;2;255;0;0m%s Error: Non-hexadecimal characters found in the result' % bad)
                        return False
                else:
                    result = r
                return result
    else:
        print('\033[38;2;0;255;0m%s This hash type is not supported.' % info)
        quit()


def get_hash_from_user():
    hash_value = input("\033[38;2;255;255;0mEnter the MD5 hash value: ").strip()
    if len(hash_value) != 32:
        print("\033[38;2;255;165;0m%s Invalid MD5 hash length. It should be 32 characters long." % bad)
        quit()
    return hash_value


def main():
    print(info + " \033[38;2;0;255;0Please enter your MD5 hash value below:")
    hash_value = get_hash_from_user()
    cracked_hash = crack(hash_value)
    if cracked_hash:
    	print('\033[38;2;0;255;0m%s Your MD5 cracked hash value is: %s' % (info, bold + cracked_hash + end))
    else:
    	print('\033[38;2;255;0;0m%s Hash was not found in any database.' % bad)



if __name__ == "__main__":
    main()
