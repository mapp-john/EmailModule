import yaml
import smtplib
from email.mime.base import MIMEBase
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
from email import encoders

########################################
# emailHTML sends an HTML email from the SMTP relay using the email address 'noreply' to the
# specified email address.
# 'to' can be a list, or a sting(separated by commas)
def emailHTML(to,subject,html,From='Automation <automation@domain.com>'):
    msg = MIMEText(html, 'html')
    msg['Subject'] = subject
    msg['From'] = From
    msg['To'] = ', '.join(to) if type(to) == list else to

    s = smtplib.SMTP('smtp.domain.com')
    s.sendmail(msg['From'], to if type(to) == list else to.split(','), msg.as_string())
    s.quit()

########################################
# emailHTMLWithAttachment sends an HTML email from the SMTP relay using the email address
# 'noreply' to the specified email address.  Attached to the email is the specified file.
# 'to' can be a list, or a sting(separated by commas)
def emailHTMLWithRenamedAttachment(to,subject,html,filename,rename,From='Automation <automation@domain.com>'):
    msg = MIMEMultipart()
    msg['Subject'] = subject
    msg['From'] = From
    msg['To'] = ', '.join(to) if type(to) == list else to

    htmlpart = MIMEText(html, 'html')
    msg.attach(htmlpart)
    with open(filename,'rb') as file:
        attachment = MIMEBase('application','octet-stream')
        attachment.set_payload(file.read())
    encoders.encode_base64(attachment)
    attachment.add_header('Content-Disposition','attachment',filename=rename)
    msg.attach(attachment)
    s = smtplib.SMTP('smtp.domain.com')
    s.sendmail(msg['From'], to if type(to) == list else to.split(','), msg.as_string())
    s.quit()

########################################
# Basic Email Function
# 'to' can be a list, or a sting(separated by commas)
def emailText(to,subject,text,From='Automation <automation@domain.com>'):
    msg = MIMEText(text)
    msg['Subject'] = subject
    msg['From'] = From
    msg['To'] = ', '.join(to) if type(to) == list else to

    s = smtplib.SMTP('smtp.domain.com')
    s.sendmail(msg['From'], to if type(to) == list else to.split(','), msg.as_string())
    s.quit()
