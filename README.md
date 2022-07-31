## Install Packages in Django
```bash
pip install django-tables2
```

## Run Local Server
```bash
D:\webapp\OneLedger>python manage.py runserver
D:\webapp\OneLedger>python manage.py runserver 0.0.0.0:8000
```
## Open Shell
```bash
D:\webapp\OneLedger>python manage.py shell
```

## Inspect DB
```python
$ python manage.py inspectdb table1 table2
```

## My First Heading
```python
ProjectsNtpc.objects.values_list('projectname','sox_pkg').filter(sox='F')
Packages.objects.values_list('id','project')
```
## Important Links
https://www.markdownguide.org/cheat-sheet/
https://www.makeareadme.com/
https://django-tables2.readthedocs.io/en/latest/

## Performing Raw Query

https://docs.djangoproject.com/en/3.2/topics/db/sql/

```python
def my_custom_sql():
    with connection.cursor() as cursor:
        cursor.execute("SELECT p.commonname as Project, P_PAY_BAREA, (p_payment_run_date) as pdate, date_format(p_payment_run_date,'%b-%y') as pdate1 , ifnull(round(sum(P_PAY_AMOUNT) / 10000000,2),0) as Amount FROM capex_pradip_data c Join Projects_ntpc p on c.P_PAY_BAREA= p.projectcode and ( P_PAY_DOC_PAYMENT_METHOD in ('M','O','A') or (p_po_number like '55000%' and P_PAY_DOC_PAYMENT_METHOD in ('C','D','L','G','B')) ) and p_payment_run_date between '2021-04-01' and '2022-03-31' and p_payment_status in ('Processed') and P_PAY_BAREA='1028' group by pdate1 ORDER BY pdate ASC")
        row = cursor.fetchall()
    return row
```

## Some Queries
```python
{{project_capex_annual_target|floatformat:2}}

CapexTarget.objects.filter(company_code__in=ProjectsNtpc.objects.values('projectcode').filter(projectname='Barh-I')).aggregate(Sum('dco'))["dco__sum"]

1. Packages.objects.values_list('project').filter(package='FGD')
2. Packages.objects.values_list('id','project').filter(id__in=ProjectsNtpc.objects.values_list('sox_pkg').filter(sox='F'))
3. D:\webapp\OneLedger>python manage.py inspectdb MileStones capex_package_po >core.test.py
4. Packages.objects.values_list('id','project').filter(id__in=ProjectsNtpc.objects.values_list('sox_pkg').filter(sox='F'))
5. ProjectsNtpc.objects.values_list('projectname','fuel').filter(fuel__in= ['Coal','Hydro'])
6. ProjectsNtpc.objects.values_list('projectname','fuel').filter(fuel__in= ['Coal','Hydro']).filter
7. (projectname__in=Milestones.objects.values_list('project').filter(milestone='TOC').exclude(achieved='A'))
```
## Working with Pandas
### Install Packaghes
```python
pip install pandas
pip install numpy
pip install openpyxl
pip install sqlalchemy
```
### Import Packaghes
```diff
- from sqlalchemy import create_engine
+ import pandas as pd
! import numpy as np
@@ import openpyxl @@
```

### Add sqlalchemy in Settings.py
```python
INSTALLED_APPS = [
    'sqlalchemy',
    'core',
    'capex',
    'mis',
    'packages',
    'projects',
    'vendors',
    'django_tables2',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'django.contrib.humanize',
]
```
### Date Time Formats
```html
https://www.programiz.com/python-programming/datetime/strftime
```

### Rename dataframe Column Name
```python
df1 = df1.rename(columns={'act_ant_date_status': 'Act/Ant Date'})
```
### Re-order Dataframe columns
```python
column_order = ["BES", "BDL", "CES", "TGES", "BHT", "BLU", "TGBU", "SBC", "TGOFC", "CHP", "AHP", "SYNC","FL","TOC","COD"]

df1 = pd.pivot_table(df, index=["Project/Unit"], columns="Milestone", values=["act_ant_date_status"], fill_value="", margins=False, margins_name='Total', sort=False, aggfunc="first")

df1_renindexed = df1.reindex(columns=column_order, level=1)

```

### Conditional Highlight DataFrame HTML Table
```
styleobj = df1_renindexed.style.applymap(lambda x: 'background-color : lightgreen;border:1px solid' if x.count(' A') > 0 else 'border:1px solid')
```

### Apply attributes to DataFrame HTML Table
```
output = styleobj.set_table_attributes('class="table table-stripped table-bordered display" style="width: 100%"')
```
### Set Precision in Dataframe values
```python
    df=pd.read_sql(mysql_qry1,dbConnection)
    df.head()
    pd.set_option('precision',0)
```

### Subtotal in Dataframe
```python

    mysql_qry1 = "select case when month(commng_date) <=3 then YEAR(commng_date) - 1 else YEAR(commng_date ) end as FY, concat(c.project,' U#',convert(c.unit,char(2))) as Project,capacity as 'Capacity' from vw_commng_mile c where achieved = 'A' ORDER BY `fy` ASC"

    df=pd.read_sql(mysql_qry1,dbConnection)
    df.head()
    pd.set_option('precision',0)

    df_pivot = pd.pivot_table(df, index=["FY", "Project"],values=["Capacity"],aggfunc=[np.sum],margins=True,margins_name='Grand Total')

    df_subtotal = pd.concat([df_pivot, df_pivot.sum(level=[0]).assign(new_col='~<span class=bg-info>Year-SubTotal</span>').set_index('new_col', append=True)]).sort_index(level=[0])
    #df_cumsum=df_subtotal.cumsum()

    styleobj =df_subtotal.style.apply(lambda x: ['background: lightgreen' if x.name == 'Year-SubTotal' else 'background: lightblue' for i in x],axis=0)

    output = styleobj.set_table_attributes('class="table p-0 table-stripped table-bordered  milestones" style="width: 100%"')
    return output.to_html()
```

### Pandas help for Subtotal

https://stackoverflow.com/questions/49881751/multiindex-pivot-table-with-subtotals-in-pandas


## ASP .NET Page LifeCycle

https://docs.microsoft.com/en-us/previous-versions/dotnet/articles/ms972976(v=msdn.10)?redirectedfrom=MSDN


## Power BI Table S.No
```
sno=calculate( countrows(table),filter(allselected(table),table[column] <= max(table[column])))
```

## Manage user RDP sessions on Windows Server 2012
```shell
PS C:\Windows\system32> quser
 USERNAME              SESSIONNAME        ID  STATE   IDLE TIME  LOGON TIME
>SomeUser              console             1  Active      none   8/16/2015 5:29 PM
PS C:\Windows\system32> logoff <sessionID>
```

## Datatables.net excel export hyperlink rendering for Safety Register Dashboard

https://stackoverflow.com/questions/40243616/jquery-datatables-export-to-excelhtml5-hyperlink-issue
https://datatables.net/extensions/buttons/examples/html5/excelTextBold.html
https://datatables.net/reference/button/excelHtml5#Built-in-styles


```javascript
buttons: [ {
			extend: 'excelHtml5',
			customize: function( xlsx ) {
				var sheet = xlsx.xl.worksheets['sheet1.xml'];

				$('row c[r^="I"]', sheet).each(function () {
						$(this).attr('t', 'str');
						$(this).append('<f>' + 'HYPERLINK("' + $('is t', this).text() + '","link")' + '</f>');
						$('is', this).remove();
						$(this).attr( 's', '4' );
				});
			}
		} ],

```

## Django template Language


### Basic Guide
https://docs.djangoproject.com/en/4.0/ref/templates/builtins/

### Icon set
http://icon-sets.iconify.design/logos/google-photos/
```
<script src="https://code.iconify.design/2/2.1.2/iconify.min.js"></script>
<span class="iconify" data-icon="logos:google-photos" style="color: red;" data-width="30"></span>
```


## Marked Down Language Code Blocks

###### Basic Formatting

https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax

###### Code blocking highlighting

https://rdmd.readme.io/docs/code-blocks


## Excel Sheet Custom Pop-up

https://www.youtube.com/watch?v=yFqJCCEsi_Y

```vbscript
Option Explicit

Private Sub Worksheet_SelectionChange(ByVal Target As Range)

    If Not Intersect(Target, Range("B4:I14")) Is Nothing Then
        Range("B4:I14").ClearComments 'Clear any existing comments in the range
        'Range("B2").Value = Target.Address
        'Range("B3").Value = Target.Column
        'Range("B4").Value = Target.Row
        'ShowPictureIcon
    Else:
        Range("B4:I14").ClearComments
        'Shapes("AddPicBtn").Visible = msoFalse
    End If
        
    'Add Formatted Comment with Dynamic Content
    If Not Intersect(Target, Range("B4:I14")) Is Nothing Then CreateFormattedComment (Target.Address)

    
    End Sub
    
Sub CreateFormattedComment(ByVal Target As String)
Dim SelRow As Long
Dim CommText As String
With Sheet2
        'SelRow = .Range("B4").Value 'Selected Row
      
        CommText = Worksheets("OngoingProjectsSummary").Range(Target).Text
        
        
        '.Range("B5").Value = Worksheets("Sheet1-summary").Range(Target).Text
        
        'Worksheets("Sheet1-summary").Range(Target).Select
        'Selection.Copy
        '.Range("B5").Select ' note that we select the whole merged cell
        'Selection.PasteSpecial Paste:=xlPasteAllUsingSourceTheme, Operation:=xlNone, SkipBlanks:=False, Transpose:=False
        
        
        'Worksheets("Sheet1-summary").Range(Target).Copy
        '.Range("B5").PasteSpecial Paste:=xlPasteFormats
        '.Range("B5").PasteSpecial Paste:=xlPasteValues
        
        
        .Range(Target).ClearComments
        .Range(Target).AddComment
        '.Range(Target).AddComment .Range("B5").Value
        
        '.Range(Target).Comment.Text Text:="OK"
        '.Range(Target).Comment.PasteSpecial Paste:=xlPasteValues
        With .Range(Target).Comment
            .Text Text:=CommText
            .Shape.Width = 300
            .Shape.Height = 200
            .Shape.AutoShapeType = msoShapeRoundedRectangle
           .Shape.Fill.ForeColor.RGB = RGB(255, 255, 153)
            '.Shape.Fill.OneColorGradient msoGradientDiagonalUp, 1, 0.23
            .Shape.TextFrame.Characters.Font.Name = "Tahoma"
            .Shape.TextFrame.Characters.Font.Bold = True
            .Shape.TextFrame.Characters.Font.Size = 10
            .Shape.TextFrame.Characters.Font.ColorIndex = 5
            .Shape.Fill.Visible = msoTrue
            .Visible = True
        End With
End With
End Sub

```

## Configuring Respberry Pi 4
1. Download Respberry Pi Imager from https://www.raspberrypi.com/software/
2. Download Full Page OS from http://unofficialpi.org/Distros/FullPageOS/
3. Insert MicroSD Card in Laptop and run Respberry Pi Imager.
4. Imager has a list of supported Raspberry OS. Choose the last option for other OS, and browse for downloaded FullPageOS
5. Select MicroSD Card and burn it.
6. Configure static IP (If required) https://www.makeuseof.com/raspberry-pi-set-static-ip/

## Setup WiFi on Raspberry Pi 4

1. Insert MicroSD Card in Laptop and Open /boot/fullpageos-wpa-supplicant.txt in a text editor.
2. Locate the WPA/WPA2 secured section in the text file.
3. Uncomment network={ to } (4 lines) by removing the # signs from the beginning of each line.
4. network={
    ssid="NETWORK-NAME"
    psk="NETWORK-PASSWORD"
}
5. Replace NETWORK-NAME with your Wi-Fi network id (inside double quotes)
6. Replace NETWORK-PASSWORD with the Wi-Fi password (inside double quotes)

For Detailed Instructions visit https://www.otot.tv/fullpageos-setup-instructions/

Now Once Connected to Internet, may run some updates
1. sudo apt-get update
2. sudo apt-get upgrade
3. sudo apt dist-upgrade


## Configure VNC on Headless Raspberry Pi 4

Now Once Connected to Internet, may run some updates
1. sudo apt-get update
2. sudo apt-get upgrade
3. sudo apt dist-upgrade

1. sudo raspi-config
2. Select Interfacing Options
	Select VNC
	For the prompt to enable VNC, select Yes (Y)
	For the confirmation, select Ok
3. Select Finish
4. For the reboot prompt, select Yes

Download Real VNC Client from https://www.realvnc.com/en/connect/download/viewer/

For Detailed instructions https://desertbot.io/blog/headless-raspberry-pi-4-remote-desktop-vnc-setup


## Change default display resolution

1. sudo raspi-config
2. Select Display
   on older versions this was under Advanced Options
3. Select Resolution
4. Select anything but the default (example: 1024x768)
5. Select Ok
6. Select Finish
7. For the reboot prompt, select Yes

## Install ZOOM on raspberry Pi 4 
https://pimylifeup.com/raspberry-pi-zoom/


## Mount One Drive in Ubuntu

1. Follow the step at https://itsfoss.com/onedriver/ . I have succesfully configured on my Ubuntu 21.10
2. For Ubuntu 21.04, you may use it by downloading from https://launchpad.net/~jstaf/+archive/ubuntu/onedriver/+packages (direct download)
3. In downloaded file, right Click-> Properties->Permission : Check Allow Executing File As Program

## Install SAP GUI in Ubuntu 21.10

1. Download [ SAP GUI for JAVA ] from https://developers.sap.com/trials-downloads.html
2. Direct Link to download is https://www.sap.com/registration/trial.f47300f6-63b8-4f22-b189-dbadd3c903d6.html?id=0050000000231062021&external-site=aHR0cHM6Ly9kZXZlbG9wZXJzLnNhcC5jb20vdHJpYWxzLWRvd25sb2Fkcy5odG1s
4. Credentials are : vsverma@ntpc.co.in & Winter@2021
5. Unrar the downloaded file (May require to install unrar via sudo apt-get install unrar)
6. install OpenJRE with sudo apt install default-jre
7. Install the C Shell and other dependencies with sudo apt-get install gcc perl csh libaio1 libc6 libstdc++6
8. Open SAP GUI extracted folder and choose the required version then run command 
9. java -jar PlatinGUI-Linux-7.50rev12.jar install
10. Installation done!
11. Open https://myapps.microsoft.com/
12. Click on SAP ERP Production
13. Rename downloaded launch.html to launch.sap
14. open SAP application -> File -> Open Connection Data Document->browse for launch.sap
15. Select MAx trusted option in next popup
16. SAP should open now 👍👍


## Install ZSCALAR VPN in Ubuntu 21.10

1. Download Zscalar client from https://d32a6ru7mhaq0c.cloudfront.net/Zscaler-linux-1.1.0.24-installer.run
2. Shared by Kuldeep Singh Sir vide email Dated 10.01.2022
3. In downloaded file, right Click-> Properties->Permission : Check Allow Executing File As Program

## HTML Table Sticky Header CSS
```html
.tableFixHead          { overflow: auto; height: 100px; }
.tableFixHead thead th { position: sticky; top: 0; z-index: 1; }

/* Just common table stuff. Really. */
table  { border-collapse: collapse; width: 100%; }
th, td { padding: 8px 16px; }
th     { background:#eee; }
```

## Project Web/Online Configuration
### Dashboard Project for Web
1. Help Document : https://support.microsoft.com/en-us/office/use-power-bi-desktop-to-connect-with-your-project-data-df4ccca1-68e9-418c-9d0f-022ac05249a2
2. Project Dashboard Template for Power BI : https://github.com/OfficeDev/Project-Power-BI-Templates
3. NTPC Dynamic 365 Dataverse URL : https://org009d3eb7.crm8.dynamics.com/ 
4. NTPC Environment Name : org009d3eb7
5. NTPC region : crm8

### Dashboard for Project Online
1. Help Document : https://support.microsoft.com/en-us/office/use-power-bi-desktop-to-connect-with-your-project-data-df4ccca1-68e9-418c-9d0f-022ac05249a2
2. Project Dashboard Template for Power BI : https://github.com/OfficeDev/Project-Power-BI-Templates
3. PWA site address URL : https://ntpccoin.sharepoint.com/sites/pwa

### Create Site for Project in MS Project Online
By default, Project Sites are no longer automatically created on first publish:
1. In PWA Settings
2. Go to Operational Policies3
3. Connected SharePoint Sites
4. click on the Settings button.
5. Create Site

## Proxy Set-up in Debian through CLI
https://computingforgeeks.com/how-to-set-system-proxy-on-debian-linux/

## DPR Table Details
1. Progress_template : Master list of all activities
2. ProgressDetails : Activity progress updates by user
3. ProgressMaster : Project wise activity meta data like complition date, Target etc

Activity ID (act_id) is important and key field

## PM server Migration SCOPE-DC
1. https://www.hostitsmart.com/blog/how-to-migrate-a-website-from-one-server-to-another/
2. https://computingforgeeks.com/how-to-set-system-proxy-on-debian-linux/

## IP CAMERA RTSP stream URL finder

https://www.ispyconnect.com/camera/mega-pixel

homepage-> more-> CameraDatabase

## Issue Tracker
```
1. do [su -] pmc:admin&42 at begining to get root authorization. this is required to edit files
2. grep -Ril "text-to-find-here" /var/www/itracker

3. /var/www/itracker/themes/default/tpl/issues/new.tpl
  (HTML of issue registration page)
4. /var/www/itracker/modules/issues/new.issues.php
  (parsing of fields of issue reg form and forward them to add_new_issue() for query creation and futher process)
  
5. /var/www/itracker/modules/issues/hooks -> func.php
 (this contains add_new_func() which generates query to add issue. Here we modified query which generates issueid from database)

6. /var/www/itracker/modules/groups/hooks/func.php
  ( This file has a function which provides package selection furing issue registration)

7. /var/www/itracker/modules/issues/hooks -> class.php
 (This contains definition of functions)
8. .tpl is HTML file and .php is code file

9. Mind Map link : https://www.mindmeister.com/map/2357743095 (Login with Google )

10. product is unit no. 61 is U#1 and so on in progression. 80 is common
11. /var/www/mis/common.php is custom commonly used functions
```
### Postfix mail troubleshooting
```
1. edit this file and add following line to it /etc/postfix/smtp_sasl_password_map
[smtp server]:[port] [mail account]:[mail account password]
10.0.14.112:25  :Ntpc@2021

Following is the SMTP configuration shared to US by EMail Group
                    credentials.UserName = ""
                    credentials.Password = "Ntpc@2021"
                    smtp.UseDefaultCredentials = False
                    smtp.Credentials = credentials
                    smtp.Port = 25
                    smtp.EnableSsl = False
2. Webmin (http://10.0.236.42:10000/)-> Postfix mail Server -> General Options
What domain to use in outbound mail : ntpc.co.in
Send outgoing mail via host : 10.0.14.112
Address that receive bccof each message : vsverma@ntpc.co.in

```

## VIM editor
1. :set number
2. :set syntax=php
3. :syntax on
4. :set autoindent

## RDP Session licensing server error
1. login to Server using Anydesk (446 365 040) from PMC user
2. open regedit and navigate to Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\RCM
3. Here you need to delete or rename [GracePeriod] registry entry
4. Right Click GracePeriod -> Permissions -> Advanced -> Click on change link at top infront of owner -> Advanced -> Find Now -> Administrators
5. Set Access permission to Full Control -> OK
6. OPen Services.msc and restart *Remote Desktop* matching services
7. Or Reboot Server
