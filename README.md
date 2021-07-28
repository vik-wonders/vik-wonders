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
1. Packages.objects.values_list('project').filter(package='FGD')
2. Packages.objects.values_list('id','project').filter(id__in=ProjectsNtpc.objects.values_list('sox_pkg').filter(sox='F'))
3. D:\webapp\OneLedger>python manage.py inspectdb MileStones capex_package_po >core.test.py
4. Packages.objects.values_list('id','project').filter(id__in=ProjectsNtpc.objects.values_list('sox_pkg').filter(sox='F'))
5. ProjectsNtpc.objects.values_list('projectname','fuel').filter(fuel__in= ['Coal','Hydro'])
6. ProjectsNtpc.objects.values_list('projectname','fuel').filter(fuel__in= ['Coal','Hydro']).filter
7. (projectname__in=Milestones.objects.values_list('project').filter(milestone='TOC').exclude(achieved='A'))
```
