import os                                               #Import Module
import time
import smtplib
import datetime
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email.mime.base import MIMEBase
from email import encoders

def mail():
    email = 'Email@Email.at'           #E-Mail von der gesendet wird
    password = 'Passwort'                             #Passwort zu der E-Mail Adresse
    send_to_email = 'Empfänger hier eintragen'      #E-Mail an die gesendet wird
    subject = 'Server not ALIVE!'                       #Betreff
    message = 'Hallo, der Server ist DOWN!'             #Nachricht
    file_location = 'server.txt'                        #Datei die gesendet wird

    msg = MIMEMultipart()
    msg['From'] = email
    msg['To'] = send_to_email
    msg['Subject'] = subject
    msg.attach(MIMEText(message, 'plain'))

    # Hier wird das Dokument angehängt
    filename = os.path.basename(file_location)
    attachment = open(file_location, "rb")
    part = MIMEBase('application', 'octet-stream')
    part.set_payload(attachment.read())
    encoders.encode_base64(part)
    part.add_header('Content-Disposition', "attachment; filename= %s" % filename)

    # Hängen Sie die Anlage an das MIMEMultipart-Objekt an
    msg.attach(part)

    server = smtplib.SMTP('smtp.gmail.com', 587)
    server.starttls()
    server.login(email, password)
    text = msg.as_string()
    server.sendmail(email, send_to_email, text)
    server.quit()

def daten():
    file = open("server.txt","a")                                           #Datei wird erstellt und geöffnet
    file.write(datetime.datetime.now().strftime("%H:%M:%S -%d.%m.%Y"))      #Zeit wird geschrieben
    file.write(" FileServer is Not Alive, IP:  ")                           #Text wird geschrieben
    file.write(ip)                                                          #Ip vom Server
    file.write("\n")                                                        #nächste Zeile
    file.write(datetime.datetime.now().strftime("%H:%M:%S -%d.%m.%Y"))
    file.write(" DNS-Server is Not Alive, IP:  ")
    file.write(ipdns)
    file.write("\n")
    file.write(datetime.datetime.now().strftime("%H:%M:%S -%d.%m.%Y"))
    file.write(" Router is Alive, IP: ")
    file.write(router)
    file.write("\n")
    file.close()                                                            #Datei wird geschlossen

def datenal():
    file = open("server.txt","a")
    file.write(datetime.datetime.now().strftime("%H:%M:%S -%d.%m.%Y"))
    file.write(" FileServer is Alive, IP:  ")
    file.write(ip)
    file.write("\n")
    file.write(datetime.datetime.now().strftime("%H:%M:%S -%d.%m.%Y"))
    file.write(" DNS-Server is Alive, IP: ")
    file.write(ipdns)
    file.write("\n")
    file.write(datetime.datetime.now().strftime("%H:%M:%S -%d.%m.%Y"))
    file.write(" Router is Alive, IP: ")
    file.write(router)
    file.write("\n")
    file.close()


x = 0                                                                      #Variable für Schleife

ip = "192.168.1.58"                                                        #IP Adressen der Server
ipdns = "192.168.1.26"
iphost = "localhost"
router = "192.168.1.1"

while x < 100:

    seconds = 300

    for i in range(seconds):                                            #Timer das alle 5 Minuten das Skript läuft
        print(str(seconds - i) + " Sekunden")
        time.sleep(1)

    print("Starte Ping Test Router")

    if os.system("ping " + router) == 0:
        print("Router ist erreichbar")
        datenal()
    else:
        print("Router NICHT erreichbar")

    print("Starte Ping Test FileServer")

    if os.system("ping " + ip) == 0:                                    #IF Verzewigung die einen Ping Test durchführt.
        print("FileServer ist erreichbar")
        datenal()
    else:
        print("FileServer NICHT erreichbar")



    print("Starte Ping Test DNS-Server")

    if os.system("ping " + ipdns) == 0:
        print("DNS Server erreichbar")
        datenal()
    elif os.system("ping " + iphost) == 0:
        print("DNS Server NICHT erreichbar")
        break
    else:
        print("Error kein NW!")



print("Sende E-Mail an Administrator!!!")                           #Skript zu Ende, da die Server nicht erreichbar sind
daten()
mail()
print("Ende")

#Luzcifer

