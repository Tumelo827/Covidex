# Covidex
COVIDEX is a real-time COVID-19 data intelligence tracker that provides global pandemic insights at a glance. With instant live updates from trusted sources, it presents essential statistics including total cases, recoveries, and fatalities, while calculating global death rates and offering estimated mortality risk by age group. Designed for clarity and precision, COVIDEX is your lightweight yet powerful tool for staying informed about the evolving impact of COVID-19 worldwide.

import requests

def fetch_covid_data():
    url = "https://disease.sh/v3/covid-19/all"
    try:
        response = requests.get(url)
        response.raise_for_status()
        return response.json()
    except requests.exceptions.RequestException as e:
        print("❌ Error fetching data:", e)
        return None

def show_summary(data):
    cases = data['cases']
    deaths = data['deaths']
    recovered = data['recovered']
    updated = data['updated']

    death_rate = (deaths / cases) * 100 if cases > 0 else 0

    print("\n🌍 CoviScope – Global COVID-19 Tracker\n")
    print(f"🕒 Last Updated: {updated}")
    print(f"📊 Total Cases: {cases:,}")
    print(f"💚 Total Recovered: {recovered:,}")
    print(f"⚰️ Total Deaths: {deaths:,}")
    print(f"📉 Global Death Rate: {death_rate:.2f}%")

    print("\n🧓 Estimated Risk by Age Group (Based on WHO/CDC estimates):")
    print(" - Age 0–17   : ~0.1% mortality")
    print(" - Age 18–49  : ~0.5% mortality")
    print(" - Age 50–64  : ~1.5% mortality")
    print(" - Age 65+    : ~5–20% mortality\n")

def main():
    data = fetch_covid_data()
    if data:
        show_summary(data)

if __name__ == "__main__":
    main()


Features:
Live data via disease.sh API
Total global cases, deaths, and recoveries
Death rate as a percentage
Estimated age-related risk breakdown
Easy to run from a terminal

