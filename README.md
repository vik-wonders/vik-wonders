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

## Mount One Drive in Ubuntu

Follow the step at https://itsfoss.com/onedriver/
I have succesfully configured on my Ubuntu 21.10

## Install SAP GUI in Ubuntu 21.10

1. Download SAP GUI for JAVA from https://developers.sap.com/trials-downloads.html
2. Unrar the downloaded file (May require to install unrar via sudo apt-get install unrar)
3. install OpenJRE with sudo apt install default-jre
4. Install the C Shell and other dependencies with sudo apt-get install gcc perl csh libaio1 libc6 libstdc++6
5. Open SAP GUI extracted folder and choose the required version then run command 
6. java -jar PlatinGUI-Linux-7.50rev12.jar install
7. Its done!
