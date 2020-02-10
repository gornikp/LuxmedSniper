# LuxmedSniper
LUX MED appointments sniper
=======================================
Simple tool to notify about available slot in LUX MED medical care service using pushover notifications. I've changed it slightly to youse Pushbullet since pushover has only a 7 day free trial. 

How to use LuxmedSniper?
--------------------

0) Install all requirements for python
```
pip install -r requirements.txt
```

1) For each specialist create configuration file (yaml format) and save it for example as my_favourite_surgeon.yml:
```
luxmed:
  email: EMAIL
  password: PASSWORD
luxmedsniper: #                     mandatory  mandatory
  doctor_locator_id: 5*4430*-1*-1 # (city_id, service_id, clinic_id, doctor_multi_identyfier) -1 means any.
                                  # You can get those ids by reading form data sent to https://portalpacjenta.luxmed.pl/PatientPortal/Reservations/Reservation/PartialSearch
                                  # on https://portalpacjenta.luxmed.pl/PatientPortal/Reservations/Reservation/Search by chrome dev tools
  lookup_time_days: 60 # How many days from now should script look at.
pushover:
  user_key: PUSHOVER_USER_KEY # Your pushover.net user key
  api_token: API_TOKEN # pushover.net App API Token
  message_template: "New visit! {AppointmentDate} at {ClinicPublicName} - {DoctorName} ({SpecialtyName}) {AdditionalInfo}"
  title: "New Lux Med visit available!" # Pushover message topic
misc:
  notifydb: ./surgeon_data # State file used to remember which notifications has been sent already
```

2) Run it (Windows)
```
python luxmedSnip.py -c /path/to/my_favourite_surgeon.yml
```
3) or run it with default settings (Windows)
```
python luxmedSnip.py
```
3) Wait for new appointment notifications in your pushbullet app on mobile :)!
