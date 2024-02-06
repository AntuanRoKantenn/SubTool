import requests
from termcolor import colored
import pyfiglet

ascii_banner = pyfiglet.figlet_format("SubDomains")
print(colored(ascii_banner, "magenta"))

def check_subdomain(subdomain, domain):
    url = f"http://{subdomain}.{domain}"
    try:
        response = requests.get(url)
        if response.status_code == 200:
            print(f"Subdomain found:{url}")
    except requests.ConnectionError:
        pass

def main():
    domain = input("Enter the domain name (example.com): ")
    wordlist_path = input("Enter the path to the wordlist file: ")

    with open(wordlist_path, "r") as f:
        for line in f:
            subdomain = line.strip()
            check_subdomain(subdomain, domain)

if __name__ == "__main__":
    main()