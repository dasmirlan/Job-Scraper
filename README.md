import requests
from bs4 import BeautifulSoup

def scrape_jobs(url):
    response = requests.get(url)
    soup = BeautifulSoup(response.content, 'html.parser')
    jobs = []
    for job in soup.find_all('div', class_='job-item'):
        title = job.find('h2').text
        company = job.find('h3').text
        location = job.find('span', class_='location').text
        jobs.append({'title': title, 'company': company, 'location': location})
    return jobs

jobs = scrape_jobs('https://example.com/jobs')
for job in jobs:
    print(f"{job['title']} at {job['company']} in {job['location']}")
