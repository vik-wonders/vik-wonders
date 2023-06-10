## Android Studio
#### Create APK
https://www.educative.io/answers/extracting-an-apk-file-from-android-studio
#### Set application version
https://forum.ionicframework.com/t/where-to-set-the-version-code-in-a-ionic-capacitor-app/192084/6
## Firebase Authentication
https://www.positronx.io/ionic-firebase-authentication-tutorial-with-examples/
https://www.positronx.io/full-angular-firebase-authentication-system/
## Django X_FRAME_OPTIONS
https://docs.djangoproject.com/en/4.1/ref/clickjacking/
## IONIC Help Docs
#### First App
https://ionicframework.com/docs/angular/your-first-app
#### Run the App
https://capacitorjs.com/docs/v2/basics/building-your-app
https://capacitorjs.com/docs/android#adding-the-android-platform
#### APP Name change
Go to created android folder and update as below

```xml
<?xml version='1.0' encoding='utf-8'?>
<resources>
    <string name="app_name">PM Tool</string>
    <string name="title_activity_main">PM Tool</string> <--This one worked
    <string name="package_name">io.ionic.starter</string>
    <string name="custom_url_scheme">io.ionic.starter</string>
</resources>
```
#### IONIC app icon change
https://www.youtube.com/watch?v=2Ce09by4qFE



```
D:\MobileApp\photo-gallery\android\app\src\main\res\values\strings.xml
```
#### New page generate
```
$ ionic generate 
$ ionic generate page
$ ionic generate page contact
$ ionic generate component contact/form
$ ionic generate component login-form --change-detection=OnPush
$ ionic generate directive ripple --skip-import
$ ionic generate service api/user
```
#### IONIC Routing How To
https://www.youtube.com/watch?v=9v_yVGb41qU&t=48s

#### IONIC Loader
https://www.positronx.io/ionic-loading-controller-tutorial-with-ion-loading-example/

#### IONIC Capacitor Browser
1. https://capacitorjs.com/docs/apis/browser
2. https://www.youtube.com/watch?v=C7pQl3VxDzE

#### IONIC Angular Toast
https://ionicframework.com/docs/api/toast
#### IONIC Menu
https://ionicframework.com/docs/api/menu#menu-toggle

#### Exit IONIC 6 app on back button
https://www.youtube.com/watch?v=yWYbYRrXsw0

app.components.ts
```ts
import { Component } from '@angular/core';
import {  Platform, IonRouterOutlet } from '@ionic/angular';
import { SplashScreen } from '@capacitor/splash-screen';
import { BackButtonService } from './services/back-button.service';
import { Router } from '@angular/router';
import { App } from '@capacitor/app';
// NavController,
@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html',
  styleUrls: ['app.component.scss'],
})
export class AppComponent {
  constructor(
    private platform: Platform,
    // private backbuttonserverice: BackButtonService,
    private router: Router,

    ) {
      this.platform.backButton.subscribeWithPriority(-1, () => {

  const currenturl = this.router.url;
          if (currenturl === '/homepage' || currenturl === '/login-page' || currenturl === '/')
          {
            // this.backbuttonserverice.init();
            App.exitApp();

          }
      });
    }

  initializeApp() {
       
}
}
```

## IIS CONFIG
https://techexpert.tips/iis/iis-disable-directory-browsing/

## Setup Python and Django
### Install Python, pipenv and VS Code
0. Tutorial Video @ https://www.youtube.com/watch?v=rHux0gMZ3Eg
1. Download latest python from www.python.org/downloads/ and Install it. Do select add to PATH option
2. ``` python --version ``` (To check version of installed python)
3. ``` pip --version ``` (To check version of installed pip)
4. ``` pip install pipenv ``` (To install python project dependency management tool)
5. ``` pipenv uninstall --all ``` (To uninstall all packages)
6. ``` pipenv --rm ``` (To remove current virtual environment)
7. Install VS Code from code.visualstudio.com
8. ``` vscode . ``` (this opens VS code with cirrent directory)
9. In VS Code serach for python in extensions and install python intellisens

### Creating Django project
1. Create a folder for django project
2. ``` pipenv install django ``` (pipenv install creates a virtual envirinment for current folder. In this case a virtual environtment will be created and django will be installed in virtual environment.
3. By default location of virtual envirnment is C:\Users\<username>\.virtualenvs\<virtual environment directory>
4. [export PIPENV_VENV_IN_PROJECT=1] Exporting this variable sets current folder as the location of virtual directory for current project [<project/.venv>]
5. ``` pipenv --venv ``` (This gives the path to the virtual environment folder of current project
6. ``` pipenv shell ``` (To activate the current virtual environment)
7. ``` django-admin startproject <Project Name> ``` (This will create a new project with specified name. With the same name a default app will also be created inside project)
8. manage.py is a wrapper around django-admin. [ Manage.py=django-admin + current project setting info ]. Therefore for management of project manage.py to be used in place of django-admin
9. ``` python manage.py runserver <port NO | 8000> ``` (This will run the server on specified port or on default port 8000. http://127.0.0.1:8000/)

### Integrated VS code Terminal
1. Here we need to configure the virtual environment python interpretor in place of golbal python interpretor
2. Go to <Python Project>
2. ``` code . ```
3. View -> Command Pallette -> Search [python interpretor]-> Enter Path
4. Here enter virtual environment path from command  ``` pipenv --venv ``` and append /Scripts/python/
5. Now open terminal View-> terminal (VS Code autometically activates virtual environment in terminal)
6. If there is an error while opening terminal regarding failure to run Activate script. Then
7. Open Powershell as admin and run  [set-executionpolicy remotesigned]. This will allow PowerShell to run all local scripts and all signed remote scripts.
8. Now can run inside terminal [ ``` python manage.py runserver ``` ]. It will work.

### Django Project Structure
1. settings.py has project wide settings
2. Run Terminal and run ``` python manage.py startapp <App Name> ``` This will add an app to django project
3. register this app under INSTALLED_APPS of settings.py
3. Each Django APP has same structure with folowing parts
	1. admin.py -> Configure admin interface for this app
	2. apps.py -> configuration for this app
	3. models.py -> Database models for this app
	4. views.py -> Request handler for this app (takes request and returns response)
	5. urls.py -> url pattern to funtion mapping

### Django Project Code Snippet
#### Project urls.py
```python
from django.contrib import admin
from django.urls import path, include
import debug_toolbar

urlpatterns = [
    path('admin/', admin.site.urls),
    path('HelloApp/', include('HelloApp.urls')),
    path('__debug__/', include('debug_toolbar.urls')),
]
```
	
1. This is like a router for url patterns from main site to apps.
2. When url is ```http://127.0.0.1:8000/HelloApp/hello/``` then it matches ```path('HelloApp/', include('HelloApp.urls')),``` and forwards control to urls.py in HelloApp

#### HelloApp urls.py
```python
from django.urls import path
from . import views

#URLConf
urlpatterns = [
    path('hello/',views.say_hello)
]
```

1. Here 2nd part of URL is matched ``` path('hello/',views.say_hello) ```
2. function say_hello() is called from HelloApp views.py

#### HelloApp Views.py
```python
from django.shortcuts import render
from django.http import HttpResponse

# Create your views here.
def say_hello(request):
    x=1
    y=2
    #return HttpResponse('Helo Dear Friends')
    return render(request,'hello.html',{'name':'Vikram'})
```

1. Here either a response text is returned by ``` return HttpResponse('Helo Dear Friends') ``` or Template is called and response is returned by ``` return render(request,'hello.html',{'name':'Vikram'}) ```

#### HelloApp hello.html in Templates folder
```html
<html><body>
{% if name %}
<h1>Hello {{name}}</h1>
{% else %}
<h1>Hello Markiv</h1>
{% endif %}
</body></html>
```

### Django applications debugging in VS Code
https://youtu.be/rHux0gMZ3Eg?t=2184

### Using Django debug Toolbar
https://youtu.be/rHux0gMZ3Eg?t=2653
All steps here ar https://django-debug-toolbar.readthedocs.io/en/latest/installation.html
1. ``` pipenv install django-debug-toolbar ```
2. Ensure INSTALLED_APPS setting has staticfiles entry in project settings.py file
```python
INSTALLED_APPS = [
    # ...
    "django.contrib.staticfiles",
    # ...
]

STATIC_URL = "static/"
```

3. Ensure TEMPLETES setting has DjangoToolbar entry
```python
TEMPLATES = [
    {
        "BACKEND": "django.template.backends.django.DjangoTemplates",
        "APP_DIRS": True,
        # ...
    }
]
```
4. MAke entry in INSTALLED_APPS
```python
INSTALLED_APPS = [
    # ...
    "debug_toolbar",
    # ...
]
```

5. Entry in Project urls.py
```python
from django.urls import include, path
import django_toolbar

urlpatterns = [
    # ...
    path('__debug__/', include('debug_toolbar.urls')),
]
```

6. ENtry in Middleware
```python
MIDDLEWARE = [
    # ...
    "debug_toolbar.middleware.DebugToolbarMiddleware",
    # ...
]
```
7. Configure Internal IPs
```python
INTERNAL_IPS = [
    # ...
    "127.0.0.1",
    # ...
]
```
THis will open Debug toolbar when django receives request from localhost
	
## Install Packages in Django
```bash
pip install django-tables2
```

## Open Shell
```bash
D:\webapp\OneLedger>pipenv shell [ This is required if virtual environment is set else below command will work]
D:\webapp\OneLedger>python manage.py shell
```

## Run Local Server
```bash
D:\webapp\OneLedger>python manage.py runserver
D:\webapp\OneLedger>python manage.py runserver 0.0.0.0:8000
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

### Folders to copy later
DBX -> Upload & CCP_files
PPMNEW -> consmanual, debian, images, Upload


## IP CAMERA RTSP stream URL finder

https://www.ispyconnect.com/camera/mega-pixel

homepage-> more-> CameraDatabase

1. IP Cam Image Capture URL -> http://10.4.8.68:9001/ipcamera.aspx?mobile=9650990882&timer=1

## Issue Tracker
```
1. do [su -] pmc:admin&42 at begining to get root authorization. this is required to edit files
2. grep -Ril "text-to-find-here" /var/www/itracker
3. http://10.0.236.42/admin/cc.php
4. http://10.0.236.42:10000
5. http://10.0.236.42/admin/admin.php
6. curl http://www.google.com

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
##### Project wise issue summary Query

```sql
SELECT g.name AS Project, gfv.value AS TYPE, COUNT(i.issueid) AS total FROM issues i JOIN groups g ON i.primary_gid = g.gid AND g.group_type = 'Ongoing' JOIN statuses s ON s.sid = i.status JOIN Packages p ON p.id = i.package JOIN issue_group_fields igf ON igf.issueid = i.issueid AND igf.gfid = 0 JOIN group_field_values gfv ON gfv.gfid = igf.gfid AND gfv.value_idx = igf.value_idx AND g.name LIKE '%' AND gfv.value LIKE '%' AND p.agency LIKE '%' WHERE i.status != 10 AND i.severity like '%' GROUP BY g.name, gfv.value ORDER BY g.name, gfv.value, total DESC
```
```sql
SELECT g.name AS Project, gfv.value AS TYPE, i.problem as summary, i.summary as title ,u1.first_name,FROM_UNIXTIME(i.opened,'%d/%m/%Y') as opened_date,datediff(now(),from_unixtime(i.opened)) as age,ss.status as status_desc, prd.product as unit,concat(p.package,'-',p.agency) as package,concat(u.first_name,'-',u.last_name) as 'Assigned To' FROM issues i JOIN groups g ON i.primary_gid = g.gid AND g.group_type = 'Ongoing' JOIN statuses s ON s.sid = i.status JOIN Packages p ON p.id = i.package JOIN issue_group_fields igf ON igf.issueid = i.issueid AND igf.gfid = 0 JOIN group_field_values gfv ON gfv.gfid = igf.gfid AND gfv.value_idx = igf.value_idx AND g.name LIKE '%' AND gfv.value LIKE '%' AND p.agency LIKE '%' JOIN statuses ss on i.status=ss.sid JOIN issue_groups ig on i.issueid=ig.issueid JOIN users u on u.userid=ig.assigned_to JOIN users u1 on u1.userid=i.opened_by JOIN products prd on i.product=prd.pid WHERE i.status != 10 AND i.severity LIKE '%' ORDER BY g.name, gfv.value
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

3. echo "Test Email message body" | mail -s "Hello from POstfix 12.09.2022 05" vsverma@ntpc.co.in
4. echo "Subject: Hello from Sendmail on 12.09.2022 05" |sendmail vsverma@ntpc.co.in
5. PHP mail() function gives -t not found error due to PHP version change from 7.3 to 7.4
6. In /etc/php/7.4/apache2/php.ini -> [mail function] section : set sendmail path as below :-
sendmail_path=/usr/sbin/sendmail -t -i
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

## PRIMS Crystal Report Configuration in New Server
1. https://www.tektutorialshub.com/crystal-reports/how-to-download-and-install-crystal-report-runtime/
2. I installed Version 13.0.18 for both x86 and x64
3. This resolved log4net assembly dependency missing error

## Particles
1. https://www.npmjs.com/package/jquery-particles
2. https://www.section.io/engineering-education/javascript-particles-effect-with-tsparticles/

## PM Website Audit
#### How to disable TLS 1.0 and TLS 1.1 on Windows Server 2008/2016
1. https://trustzone.com/knowledge-base/how-to-disable-tls-1-0-and-tls-1-1-on-windows-server-2008-2016/

#### Enable TLS 1.2 on WIndows Server 2019
1. https://thesecmaster.com/how-to-enable-tls-1-2-and-tls-1-3-on-windows-server/
#### How to protect your IIS webserver from SWEET32 bug
1. https://www.youtube.com/watch?v=nF2RLAbvfrY
#### Help for many audit points
1. https://www.yeahhub.com/iis-server-hardening-banner-grabbing-prevention-techniques/
2. https://techexpert.tips/iis/iis-disable-directory-browsing/
#### Disble Server Version from response
```
In Web.Config
  <system.webServer>
	  <security>
		  <requestFiltering removeServerHeader="true" />
	  </security>
	    // Rest-of-the-content
  </system.webServer>
```
#### Disable X-Powered-By PHP versin Response Header
1. https://memorynotfound.com/remove-x-powered-by-php-from-http-response-header/#:~:text=Look%20for%20the%20expose_php%20attribute,from%20the%20HTTP%20Response%20Header.
	    
#### Disbale ASP .NET Version from response
```
<system.web>
	    <httpRuntime enableVersionHeader="false" />
	    // most probably no need to create separate httpRuntime element. Ass enableVersionHeader="false" to existing element
<system.web>

```
#### Disable debugging
```
<compilation debug="false" targetFramework="4.8">
```
	    
	    
	    
## Project/ Unit ongoing/completed logic
1. units.completed= -1 (Not Completed)
2. units.completed= 0 (Completed)
3. units.completed= 99 (scrapped LPHPP)
4. units.completed= -99 (Work stopped Khasiabara, Lata Tapovan)
5. Logic 99 or others
6. units.zerodate is common for all units for a stage
7. units.zerodate is null (Never started)
8. If TOC milestone is not achieved then unit is under construction i.e. ongoing

## Hindrance Register Logic
```sql
SELECT
    IF(
    STATUS
        = '',
        (
            CASE WHEN raised_by = 'NTPC' AND start_acceptance_agency = 0 THEN 'Acceptance / Rejection pending by Agency' WHEN raised_by = 'Agency' AND start_acceptance_ntpc = 0 THEN 'Acceptance / Rejection pending by NTPC' WHEN resolution = '' THEN 'Resolution pending' WHEN ISNULL(end_date) THEN 'End date pending' ELSE 'Closed'
        END
),
STATUS
) AS
STATUS
FROM
    Hindrance_reg
WHERE
    id = 1976
```

For Hindrance to be closed, 04 conditions to be fulfilled
1. NTPC and Agency, both must accept
2. Resolution must be given i.e. resolution field should not be empty
3. End date must be provided

## DMS View Logic
1. User Role : can view all his created documents for specified project
2. EIC Role : User Role + Packages assigned to him
3. ppm : all documents of project assigned to him

	    
## Encrypt data in MySql
```
INSERT INTO `testtable`(`empno`, `password`, `name`) VALUES ('10', TO_BASE64(AES_ENCRYPT('mypassword','mykey')),'vikram')
SELECT `id`, `empno`, AES_DECRYPT(FROM_BASE64(password), 'mykey'), `name`, `time_stamp` FROM `testtable` WHERE id=7
```
1. Here 'mypassord' is the value I want to encrypt. This is being insertted into password column
2. 'mykey' is the Secret key
3. https://www.percona.com/blog/column-level-encryption-in-mysql/
	    
## WhatsApp API
1. https://user.ultramsg.com/index.php
2. Login id : singh.markiv@gmail.com, Mob-9471001337, Password : Google Generated. Saved in Google Profile
3. Create Instanace
4. Authenticated instance with NTPC PMC WhatsApp Account-9650990154 (i.e. Lined the devices using QR Code)
5. API URL : https://api.ultramsg.com/instance42842/
6. Instance ID : instance42842
7. Token : xxu2h87vcmps4rtb

* Demo is limited to 100 Messages per Day.
* Session logs out after 14 Days
* Instance acn be authenticated using any WhatsApp Account

	    
```
using RestSharp;
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Drawing;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;


namespace WhatsAPP_API
{
	public partial class Form1 : Form
	{
		public Form1()
		{
			InitializeComponent();
		}

		private void Form1_Load(object sender, EventArgs e)
		{
			byte[] AsBytes = File.ReadAllBytes("C:\\Users\\ftpuser\\Downloads\\NTPC-BHEL Progress Report.pdf");

			String AsBase64String = Convert.ToBase64String(AsBytes);

			///////////

			var url = "https://api.ultramsg.com/instance42738/messages/document";

            var client =

				new RestClient(url);

			var request = new RestRequest(url, Method.Post);

			request.AddHeader("content-type", "application/x-www-form-urlencoded");

			request.AddParameter("token", "j4p6v7ff2gs4eowz", ParameterType.GetOrPost);

			request.AddParameter("to", "+919471001337", ParameterType.GetOrPost);

			request.AddParameter("document", AsBase64String, ParameterType.GetOrPost);

			request.AddParameter("caption", "Hello", ParameterType.GetOrPost);

			request.AddParameter("filename", "NTPC-BHEL Progress Report.pdf");





			RestResponse response = client.Execute(request);

		}
	}
}

```

## Week No to date mapping
	    https://www.epochconverter.com/weeks/2023
	    
## SQL Validator and SQL generator

https://www.eversql.com/sql-syntax-check-validator/

	    
## SAP HANA Features
https://skillstek.com/sap-versions/

## Badminton Rules
https://www.bbc.co.uk/bitesize/guides/zp9ck7h/revision/3
	    
## Datatable.net conditional cell background color
```javascript
            $('#tb').DataTable({
                "order": [0, "asc"], "paging": true, "lengthMenu": [10, 25, 50, "All"], "iDisplayLength": 200, "searching": true, "fixedHeader": true, dom: 'Bfrtip', buttons: ['excel',
                    {
                        extend: 'pdfHtml5',
                        orientation: 'landscape',
                        pageSize: 'LEGAL'
                    }
                ], rowGroup: {

                    dataSrc: 0
                },
                columnDefs: [{ targets: 0, visible: false }],
                'rowCallback': function (row, data, index) {
                    //console.log("Data :" + data[3] + ", type : " + typeof data[3]);
                 if (data[3] == "0") {
                     $(row).find('td:eq(2)').css('background', 'red');
                     //$(row).css('color', 'red');
                }
                }
            });
```
## CAPTCHA
1. https://www.c-sharpcorner.com/article/asp-net-webform-user-registration-with-captcha/
2. https://help.syncfusion.com/aspnet/captcha/getting-started

## Merge Excell sheets into one
https://excelchamps.com/blog/merge-excel-files-one-workbook/

## ASP .NET Password Validators/ Strong Password Policy
1. https://www.aspsnippets.com/Articles/Implement-Password-Policy-using-Regular-Expressions-and-ASPNet-RegularExpression-Validator.aspx


## Engineering Drawings release categories
* CAT-I : Approved 
* CAT-II : Approved with Comment
* CAT-II : Rejected
* CAT-IV & CAT-IV-R : These are Auto Approved. For information Only

## Create Web API or Web Service
1. https://www.tutorialsteacher.com/webapi/request-response-data-formats-in-web-api
2. https://dotnettutorials.net/lesson/creating-web-api-application/

## Digital Signature on Multiple PDF Files in single go
https://www.youtube.com/watch?v=RKG5g1rDmQc
