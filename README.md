## Run Local Server
```bash
D:\webapp\OneLedger>python manage.py runserver
```
## Open Shell
```bash
D:\webapp\OneLedger>python manage.py shell
```

## Inspect DB
```
$ python manage.py inspectdb table1 table2
```

## My First Heading
```
ProjectsNtpc.objects.values_list('projectname','sox_pkg').filter(sox='F')
Packages.objects.values_list('id','project')
```
## Important Links
```bash
https://www.markdownguide.org/cheat-sheet/
https://www.makeareadme.com/
https://django-tables2.readthedocs.io/en/latest/
```
## Install Packages in Django
```bash
pip install django-tables2
```

## Some Queries
```
- Packages.objects.values_list('project').filter(package='FGD')
- Packages.objects.values_list('id','project').filter(id__in=ProjectsNtpc.objects.values_list('sox_pkg').filter(sox='F'))
- D:\webapp\OneLedger>python manage.py inspectdb MileStones capex_package_po >core.test.py
- Packages.objects.values_list('id','project').filter(id__in=ProjectsNtpc.objects.values_list('sox_pkg').filter(sox='F'))
- ProjectsNtpc.objects.values_list('projectname','fuel').filter(fuel__in= ['Coal','Hydro'])
- ProjectsNtpc.objects.values_list('projectname','fuel').filter(fuel__in= ['Coal','Hydro']).filter
-(projectname__in=Milestones.objects.values_list('project').filter(milestone='TOC').exclude(achieved='A'))
```
