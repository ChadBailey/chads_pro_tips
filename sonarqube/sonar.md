
# Python General Notes

- sonarqube uses a plugin for python, the source for this plugin can be found 
at https://github.com/SonarSource/sonar-python

- Sonar does not actually calculate coverage, it expects an xml report 
supplied to it, specified with `sonar.python.coverage.reportPath` in 
`sonar-project.properties`

 - [coverage.py](https://coverage.readthedocs.io/en/v4.5.x/cmd.html#xml-reporting) 
is the tool typically used for calculating code coverage in python

 - The xml file is expected to be in 
[Cobertura](https://cobertura.github.io/cobertura/) format

 - Compatible xml can be generated with coverage.py via 
 `coverage xml -o "filename.xml"`

