    Copyright(c) 2019
    Author: Chaitanya Tejaswi (github.com/CRTejaswi)    License: GPL v3.0+

# Analysis: StackOverFlow Developer Survey
> Based on the [tutorial](https://www.youtube.com/watch?v=_P7X8tMplsw) by [Corey Schafer](https://coreyms.com/).

[[VIDEO]](https://www.youtube.com/watch?v=_P7X8tMplsw)
[[DATASET]](https://insights.stackoverflow.com/survey)


<details>
<summary> v0.1 </summary>

> CHANGES: Check for entries.

``` py
#!/usr/bin/env python3
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        rows = csv.DictReader(f)
        entry = next(rows)
    return entry

if __name__ == '__main__':
    entry = CSVReader('data/survey_results_public.csv')
```
```
$ py -i main.py
>>> entry['Respondent']; entry['Country']; entry['DevEnviron'];
'1'
'United Kingdom'
'IntelliJ;Notepad++;PyCharm'
```
</details>

<details>
<summary> v0.2a </summary>

> CHANGES: Check how many people code as a hobby.
Uses `dict()` to implement counter.

``` py
#!/usr/bin/env python3
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        rows = csv.DictReader(f)
        counter = {'Yes': 0, 'No': 0}
        for row in rows:
            counter[row['Hobbyist']] += 1
    return counter

if __name__ == '__main__':
    entry = CSVReader('data/survey_results_public.csv')
```
```
$ py -i main.py
>>> entry['Yes']; entry['No'];
71257
17626
>>> total = entry['Yes'] + entry['No']
>>> yes, no = round(entry['Yes']/total * 100, 2), round(entry['No']/total * 100, 2)
>>> print(f'Yes: {yes}%, No: {no}%')
Yes: 80.17%, No: 19.83%
```
</details>

<details>
<summary> v0.2b </summary>

> CHANGES: Uses `defaultdict` instead of `dict()`.

``` py
#!/usr/bin/env python3
from collections import defaultdict
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        rows = csv.DictReader(f)
        counter = defaultdict(int)
        for row in rows:
            counter[row['Hobbyist']] += 1
    return counter

if __name__ == '__main__':
    entry = CSVReader('data/survey_results_public.csv')
```
```
$ py -i main.py
>>> entry['Yes']; entry['No'];
71257
17626
>>> total = entry['Yes'] + entry['No']
>>> yes, no = round(entry['Yes']/total * 100, 2), round(entry['No']/total * 100, 2)
>>> print(f'Yes: {yes}%, No: {no}%')
Yes: 80.17%, No: 19.83%
```
</details>

<details>
<summary> v0.2c </summary>

> CHANGES: Uses `Counter` instead of `defaultdict`.

``` py
#!/usr/bin/env python3
from collections import Counter
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        rows = csv.DictReader(f)
        counter = Counter()
        for row in rows:
            counter[row['Hobbyist']] += 1
    return counter

if __name__ == '__main__':
    entry = CSVReader('data/survey_results_public.csv')
```
```
$ py -i main.py
>>> entry['Yes']; entry['No'];
71257
17626
>>> total = entry['Yes'] + entry['No']
>>> yes, no = round(entry['Yes']/total * 100, 2), round(entry['No']/total * 100, 2)
>>> print(f'Yes: {yes}%, No: {no}%')
Yes: 80.17%, No: 19.83%
```
</details>

<details>
<summary> v0.3 </summary>

> CHANGES: Display Question-Codes alongwith actual Questions asked in survey.

- [ ] Save entries as CSV, JSON & PDF.

``` py
#!/usr/bin/env python3
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        rows = csv.reader(f)
        next(rows)
        return list(rows)

if __name__ == '__main__':
    entries = CSVReader('data/survey_results_schema.csv')
    for entry in entries:
        print(f'{entry[0]:25}: "{entry[1]}"')

```
```
$ py main.py
Respondent               : "Randomized respondent ID number (not in order of survey response time)"
MainBranch               : "Which of the following options best describes you today? Here, by "developer" we mean "someone who writes code.""
Hobbyist                 : "Do you code as a hobby?"
OpenSourcer              : "How often do you contribute to open source?"
OpenSource               : "How do you feel about the quality of open source software (OSS)?"
Employment               : "Which of the following best describes your current employment status?"
Country                  : "In which country do you currently reside?"
Student                  : "Are you currently enrolled in a formal, degree-granting college or university program?"
EdLevel                  : "Which of the following best describes the highest level of formal education that youâ€™ve completed?"
UndergradMajor           : "What was your main or most important field of study?"
EduOther                 : "Which of the following types of non-degree education have you used or participated in? Please select all that apply."
OrgSize                  : "Approximately how many people are employed by the company or organization you work for?"
DevType                  : "Which of the following describe you? Please select all that apply."
YearsCode                : "Including any education, how many years have you been coding?"
Age1stCode               : "At what age did you write your first line of code or program? (E.g., webpage, Hello World, Scratch project)"
YearsCodePro             : "How many years have you coded professionally (as a part of your work)?"
CareerSat                : "Overall, how satisfied are you with your career thus far?"
JobSat                   : "How satisfied are you with your current job? (If you work multiple jobs, answer for the one you spend the most hours on.)"
MgrIdiot                 : "How confident are you that your manager knows what theyâ€™re doing?"
MgrMoney                 : "Do you believe that you need to be a manager to make more money?"
MgrWant                  : "Do you want to become a manager yourself in the future?"
JobSeek                  : "Which of the following best describes your current job-seeking status?"
LastHireDate             : "When was the last time that you took a job with a new employer?"
LastInt                  : "In your most recent successful job interview (resulting in a job offer), you were asked to... (check all that apply)"
FizzBuzz                 : "Have you ever been asked to solve FizzBuzz in an interview?"
JobFactors               : "Imagine that you are deciding between two job offers with the same compensation, benefits, and location. Of the following factors, which 3 are MOST important to you?"
ResumeUpdate             : "Think back to the last time you updated your resumÃ©, CV, or an online profile on a job site. What is the PRIMARY reason that you did so?"
CurrencySymbol           : "Which currency do you use day-to-day? If your answer is complicated, please pick the one you're most comfortable estimating in."
CurrencyDesc             : "Which currency do you use day-to-day? If your answer is complicated, please pick the one you're most comfortable estimating in."
CompTotal                : "What is your current total compensation (salary, bonuses, and perks, before taxes and deductions), in `CurrencySymbol`? Please enter a whole number in the box below, without any punctuation. If you are paid hourly, please estimate an equivalent weekly, monthly, or yearly salary. If you prefer not to answer, please leave the box empty."
CompFreq                 : "Is that compensation weekly, monthly, or yearly?"
ConvertedComp            : "Salary converted to annual USD salaries using the exchange rate on 2019-02-01, assuming 12 working months and 50 working weeks."
WorkWeekHrs              : "On average, how many hours per week do you work?"
WorkPlan                 : "How structured or planned is your work?"
WorkChallenge            : "Of these options, what are your greatest challenges to productivity as a developer? Select up to 3:"
WorkRemote               : "How often do you work remotely?"
WorkLoc                  : "Where would you prefer to work?"
ImpSyn                   : "For the specific work you do, and the years of experience you have, how do you rate your own level of competence?"
CodeRev                  : "Do you review code as part of your work?"
CodeRevHrs               : "On average, how many hours per week do you spend on code review?"
UnitTests                : "Does your company regularly employ unit tests in the development of their products?"
PurchaseHow              : "How does your company make decisions about purchasing new technology (cloud, AI, IoT, databases)?"
PurchaseWhat             : "What level of influence do you, personally, have over new technology purchases at your organization?"
LanguageWorkedWith       : "Which of the following programming, scripting, and markup languages have you done extensive development work in over the past year, and which do you want to work in over the next year?  (If you both worked with the language and want to continue to do so, please check both boxes in that row.)"
LanguageDesireNextYear   : "Which of the following programming, scripting, and markup languages have you done extensive development work in over the past year, and which do you want to work in over the next year?  (If you both worked with the language and want to continue to do so, please check both boxes in that row.)"
DatabaseWorkedWith       : "Which of the following database environments have you done extensive development work in over the past year, and which do you want to work in over the next year?   (If you both worked with the database and want to continue to do so, please check both boxes in that row.)"
DatabaseDesireNextYear   : "Which of the following database environments have you done extensive development work in over the past year, and which do you want to work in over the next year?   (If you both worked with the database and want to continue to do so, please check both boxes in that row.)"
PlatformWorkedWith       : "Which of the following platforms have you done extensive development work for over the past year?   (If you both developed for the platform and want to continue to do so, please check both boxes in that row.)"
PlatformDesireNextYear   : "Which of the following platforms have you done extensive development work for over the past year?   (If you both developed for the platform and want to continue to do so, please check both boxes in that row.)"
WebFrameWorkedWith       : "Which of the following web frameworks have you done extensive development work in over the past year, and which do you want to work in over the next year? (If you both worked with the framework and want to continue to do so, please check both boxes in that row.)"
WebFrameDesireNextYear   : "Which of the following web frameworks have you done extensive development work in over the past year, and which do you want to work in over the next year? (If you both worked with the framework and want to continue to do so, please check both boxes in that row.)"
MiscTechWorkedWith       : "Which of the following other frameworks, libraries, and tools have you done extensive development work in over the past year, and which do you want to work in over the next year? (If you both worked with the technology and want to continue to do so, please check both boxes in that row.)"
MiscTechDesireNextYear   : "Which of the following other frameworks, libraries, and tools have you done extensive development work in over the past year, and which do you want to work in over the next year? (If you both worked with the technology and want to continue to do so, please check both boxes in that row.)"
DevEnviron               : "Which development environment(s) do you use regularly?  Please check all that apply."
OpSys                    : "What is the primary operating system in which you work?"
Containers               : "How do you use containers (Docker, Open Container Initiative (OCI), etc.)?"
BlockchainOrg            : "How is your organization thinking about or implementing blockchain technology?"
BlockchainIs             : "Blockchain / cryptocurrency technology is primarily:"
BetterLife               : "Do you think people born today will have a better life than their parents?"
ITperson                 : "Are you the "IT support person" for your family?"
OffOn                    : "Have you tried turning it off and on again?"
SocialMedia              : "What social media site do you use the most?"
Extraversion             : "Do you prefer online chat or IRL conversations?"
ScreenName               : "What do you call it?"
SOVisit1st               : "To the best of your memory, when did you first visit Stack Overflow?"
SOVisitFreq              : "How frequently would you say you visit Stack Overflow?"
SOVisitTo                : "I visit Stack Overflow to... (check all that apply)"
SOFindAnswer             : "On average, how many times a week do you find (and use) an answer on Stack Overflow?"
SOTimeSaved              : "Think back to the last time you solved a coding problem using Stack Overflow, as well as the last time you solved a problem using a different resource. Which was faster?"
SOHowMuchTime            : "About how much time did you save? If you're not sure, please use your best estimate."
SOAccount                : "Do you have a Stack Overflow account?"
SOPartFreq               : "How frequently would you say you participate in Q&A on Stack Overflow? By participate we mean ask, answer, vote for, or comment on questions."
SOJobs                   : "Have you ever used or visited Stack Overflow Jobs?"
EntTeams                 : "Have you ever used Stack Overflow for Enterprise or Stack Overflow for Teams?"
SOComm                   : "Do you consider yourself a member of the Stack Overflow community?"
WelcomeChange            : "Compared to last year, how welcome do you feel on Stack Overflow?"
SONewContent             : "Would you like to see any of the following on Stack Overflow? Check all that apply."
Age                      : "What is your age (in years)? If you prefer not to answer, you may leave this question blank."
Gender                   : "Which of the following do you currently identify as? Please select all that apply. If you prefer not to answer, you may leave this question blank."
Trans                    : "Do you identify as transgender?"
Sexuality                : "Which of the following do you currently identify as? Please select all that apply. If you prefer not to answer, you may leave this question blank."
Ethnicity                : "Which of the following do you identify as? Please check all that apply. If you prefer not to answer, you may leave this question blank."
Dependents               : "Do you have any dependents (e.g., children, elders, or others) that you care for?"
SurveyLength             : "How do you feel about the length of the survey this year?"
SurveyEase               : "How easy or difficult was this survey to complete?"
```
</details>


### Answering Common Questions

<details>
<summary>
    <b>
    Q: Among the people who took this survey, what are the popular programming languages?
    </b>
</summary>

> CHANGES: Among the people who took this survey, what are the popular programming languages?

``` py
#!/usr/bin/env python3
from collections import Counter
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        devType_info = {}
        rows = csv.DictReader(f)
        for row in rows:
            devTypes = row['DevType'].split(';')
            languages = row['LanguageWorkedWith'].split(';')
            for devType in devTypes:
                devType_info.setdefault(devType, {
                    'total': 0,
                    'userCount': Counter()
                })
                devType_info[devType]['userCount'].update(languages)
                devType_info[devType]['total'] += 1
    return devType_info

if __name__ == '__main__':
    entries = CSVReader('data/survey_results_public.csv')
    for devType, info in entries.items():
        print(f'{devType:50}')
        for language, value in info['userCount'].most_common():
            userCount = round((value / info['total']) * 100, 2)
            print(f'\t{language:22}: {userCount:8}% ({value:5} Users)')
```
```
$ py main.py
JavaScript            : 66.63%
HTML/CSS              : 62.4%
SQL                   : 53.49%
Python                : 41.0%
Java                  : 40.41%
Bash/Shell/PowerShell : 35.99%
C#                    : 30.49%
PHP                   : 25.91%
C++                   : 23.09%
TypeScript            : 20.84%
C                     : 20.27%
Other(s):             : 8.91%
Ruby                  : 8.25%
Go                    : 8.1%
Assembly              : 6.56%
Swift                 : 6.46%
Kotlin                : 6.32%
R                     : 5.68%
VBA                   : 5.38%
Objective-C           : 4.72%
Scala                 : 3.72%
Rust                  : 3.14%
Dart                  : 1.89%
NA                    : 1.48%
Elixir                : 1.42%
Clojure               : 1.41%
WebAssembly           : 1.14%
F#                    : 1.09%
Erlang                : 0.87%
```
</details>

<details>
<summary>
    <b>
    Q: Among the people who took this survey, what are the popular programming languages based on developer-type?
    </b>
</summary>

> CHANGES: Among the people who took this survey, what are the popular programming languages based on developer-type?

``` py
#!/usr/bin/env python3
from collections import Counter
import csv


def CSVReader(filename):
    with open(filename, 'r', encoding='utf-8') as f:
        devType_info = {}
        rows = csv.DictReader(f)
        for row in rows:
            devTypes = row['DevType'].split(';')
            languages = row['LanguageWorkedWith'].split(';')
            for devType in devTypes:
                devType_info.setdefault(devType, {
                    'total': 0,
                    'userCount': Counter()
                })
                devType_info[devType]['userCount'].update(languages)
                devType_info[devType]['total'] += 1
    return devType_info


if __name__ == '__main__':
    entries = CSVReader('data/survey_results_public.csv')
    for devType, info in entries.items():
        print(f'{devType:50}')
        for language, value in info['userCount'].most_common():
            userCount = round((value / info['total']) * 100, 2)
            print(f'\t{language:22}: {userCount}%')
```
```
$ py main.py

B:\CRTejaswi\Programs\All\Surveys>py -i main.py
NA
        HTML/CSS              :     54.9% ( 4144 Users)
        Python                :    51.09% ( 3856 Users)
        JavaScript            :    50.58% ( 3818 Users)
        Java                  :    42.71% ( 3224 Users)
        C++                   :    35.02% ( 2643 Users)
        SQL                   :    34.72% ( 2621 Users)
        C                     :    32.55% ( 2457 Users)
        Bash/Shell/PowerShell :    30.71% ( 2318 Users)
        C#                    :    23.97% ( 1809 Users)
        PHP                   :    23.33% ( 1761 Users)
        Assembly              :    13.51% ( 1020 Users)
        Other(s):             :    10.33% (  780 Users)
        TypeScript            :      8.7% (  657 Users)
        NA                    :     6.77% (  511 Users)
        Go                    :     5.99% (  452 Users)
        VBA                   :     5.52% (  417 Users)
        Ruby                  :     5.42% (  409 Users)
        Swift                 :     5.41% (  408 Users)
        R                     :     5.34% (  403 Users)
        Kotlin                :     5.11% (  386 Users)
        Rust                  :     4.93% (  372 Users)
        Objective-C           :     2.94% (  222 Users)
        Dart                  :     2.19% (  165 Users)
        Scala                 :     1.99% (  150 Users)
        WebAssembly           :     1.71% (  129 Users)
        Clojure               :     1.06% (   80 Users)
        F#                    :     1.01% (   76 Users)
        Elixir                :     0.95% (   72 Users)
        Erlang                :     0.78% (   59 Users)
Developer, desktop or enterprise applications
        JavaScript            :    67.84% (11748 Users)
        HTML/CSS              :    64.55% (11178 Users)
        SQL                   :    63.56% (11006 Users)
        C#                    :    53.69% ( 9297 Users)
        Java                  :    44.69% ( 7739 Users)
        Bash/Shell/PowerShell :    38.95% ( 6745 Users)
        Python                :    36.23% ( 6274 Users)
        C++                   :    32.34% ( 5600 Users)
        C                     :    24.76% ( 4287 Users)
        PHP                   :    24.63% ( 4265 Users)
        TypeScript            :    24.45% ( 4233 Users)
        Other(s):             :    12.04% ( 2084 Users)
        VBA                   :     9.66% ( 1672 Users)
        Assembly              :     8.22% ( 1423 Users)
        Go                    :     7.37% ( 1277 Users)
        Swift                 :     6.31% ( 1093 Users)
        Kotlin                :     5.97% ( 1033 Users)
        Objective-C           :     5.94% ( 1028 Users)
        Ruby                  :      5.8% ( 1004 Users)
        R                     :     3.82% (  661 Users)
        Rust                  :     3.62% (  627 Users)
        Scala                 :      3.1% (  536 Users)
        Dart                  :     2.18% (  377 Users)
        F#                    :     2.08% (  360 Users)
        WebAssembly           :     1.86% (  322 Users)
        Clojure               :     1.26% (  219 Users)
        Elixir                :     1.11% (  192 Users)
        Erlang                :     0.96% (  167 Users)
        NA                    :      0.7% (  121 Users)
Developer, front-end
        JavaScript            :    87.72% (23376 Users)
        HTML/CSS              :    83.62% (22285 Users)
        SQL                   :    58.65% (15630 Users)
        Java                  :     37.6% (10021 Users)
        PHP                   :    35.94% ( 9578 Users)
        C#                    :    34.44% ( 9179 Users)
        TypeScript            :    33.24% ( 8858 Users)
        Bash/Shell/PowerShell :    33.21% ( 8850 Users)
        Python                :    31.68% ( 8442 Users)
        C++                   :    19.36% ( 5158 Users)
        C                     :    16.58% ( 4418 Users)
        Ruby                  :     8.63% ( 2301 Users)
        Other(s):             :     7.93% ( 2113 Users)
        Go                    :     6.98% ( 1859 Users)
        Swift                 :     6.75% ( 1798 Users)
        VBA                   :     5.66% ( 1508 Users)
        Kotlin                :     5.64% ( 1502 Users)
        Assembly              :     5.11% ( 1361 Users)
        Objective-C           :     5.07% ( 1351 Users)
        R                     :     3.08% (  820 Users)
        Rust                  :     2.54% (  677 Users)
        Dart                  :     2.34% (  624 Users)
        Scala                 :     2.29% (  610 Users)
        Elixir                :     1.62% (  433 Users)
        WebAssembly           :     1.47% (  391 Users)
        Clojure               :     1.38% (  367 Users)
        F#                    :     1.12% (  298 Users)
        Erlang                :     0.84% (  225 Users)
        NA                    :     0.75% (  200 Users)
Designer
        HTML/CSS              :    78.88% ( 7243 Users)
        JavaScript            :    78.33% ( 7192 Users)
        SQL                   :    60.18% ( 5526 Users)
        PHP                   :    40.23% ( 3694 Users)
        Java                  :    39.44% ( 3621 Users)
        C#                    :    35.46% ( 3256 Users)
        Python                :    35.26% ( 3238 Users)
        Bash/Shell/PowerShell :    32.97% ( 3027 Users)
        C++                   :    26.56% ( 2439 Users)
        C                     :    23.42% ( 2150 Users)
        TypeScript            :    23.02% ( 2114 Users)
        Other(s):             :    10.92% ( 1003 Users)
        VBA                   :      8.6% (  790 Users)
        Assembly              :     8.35% (  767 Users)
        Ruby                  :     7.91% (  726 Users)
        Swift                 :     7.62% (  700 Users)
        Objective-C           :     6.14% (  564 Users)
        Go                    :     6.09% (  559 Users)
        Kotlin                :     5.69% (  522 Users)
        R                     :     4.26% (  391 Users)
        Dart                  :     2.72% (  250 Users)
        Rust                  :     2.37% (  218 Users)
        Scala                 :      2.3% (  211 Users)
        WebAssembly           :     1.72% (  158 Users)
        Elixir                :     1.34% (  123 Users)
        NA                    :     1.27% (  117 Users)
        Clojure               :     1.23% (  113 Users)
        F#                    :     1.19% (  109 Users)
        Erlang                :     0.97% (   89 Users)
Developer, back-end
        JavaScript            :    72.23% (29372 Users)
        HTML/CSS              :    65.42% (26605 Users)
        SQL                   :    64.01% (26031 Users)
        Java                  :    44.03% (17904 Users)
        Python                :    40.67% (16537 Users)
        Bash/Shell/PowerShell :    40.04% (16281 Users)
        C#                    :     34.6% (14071 Users)
        PHP                   :    30.73% (12498 Users)
        TypeScript            :    23.18% ( 9427 Users)
        C++                   :    22.28% ( 9059 Users)
        C                     :    19.09% ( 7761 Users)
        Go                    :    10.61% ( 4313 Users)
        Ruby                  :     9.39% ( 3820 Users)
        Other(s):             :     8.83% ( 3591 Users)
        Kotlin                :     6.22% ( 2530 Users)
        Assembly              :     5.79% ( 2353 Users)
        VBA                   :     5.15% ( 2094 Users)
        Scala                 :      5.1% ( 2072 Users)
        Swift                 :     5.08% ( 2066 Users)
        R                     :     4.05% ( 1647 Users)
        Objective-C           :     3.89% ( 1583 Users)
        Rust                  :     3.55% ( 1445 Users)
        Elixir                :     1.89% (  770 Users)
        Dart                  :     1.84% (  748 Users)
        Clojure               :      1.7% (  691 Users)
        F#                    :     1.39% (  566 Users)
        WebAssembly           :     1.24% (  505 Users)
        Erlang                :     1.19% (  483 Users)
        NA                    :     0.62% (  253 Users)
Developer, full-stack
        JavaScript            :    86.15% (36376 Users)
        HTML/CSS              :    78.94% (33329 Users)
        SQL                   :    65.54% (27674 Users)
        Java                  :    40.74% (17201 Users)
        Bash/Shell/PowerShell :    37.91% (16005 Users)
        C#                    :     37.5% (15832 Users)
        Python                :    36.49% (15406 Users)
        PHP                   :    32.75% (13826 Users)
        TypeScript            :    32.28% (13629 Users)
        C++                   :    18.24% ( 7700 Users)
        C                     :    15.85% ( 6694 Users)
        Ruby                  :    10.38% ( 4381 Users)
        Go                    :     8.98% ( 3793 Users)
        Other(s):             :     7.87% ( 3323 Users)
        Kotlin                :     5.86% ( 2474 Users)
        Swift                 :     5.79% ( 2446 Users)
        VBA                   :     5.19% ( 2192 Users)
        Assembly              :     4.94% ( 2086 Users)
        Objective-C           :     4.25% ( 1796 Users)
        R                     :     3.68% ( 1553 Users)
        Scala                 :     3.56% ( 1503 Users)
        Rust                  :     2.98% ( 1259 Users)
        Dart                  :     2.19% (  925 Users)
        Elixir                :     1.92% (  809 Users)
        Clojure               :     1.73% (  731 Users)
        WebAssembly           :     1.44% (  606 Users)
        F#                    :     1.31% (  553 Users)
        Erlang                :     0.97% (  410 Users)
        NA                    :     0.53% (  224 Users)
Academic researcher
        Python                :    61.06% ( 3621 Users)
        HTML/CSS              :    55.87% ( 3313 Users)
        JavaScript            :    54.25% ( 3217 Users)
        SQL                   :    47.55% ( 2820 Users)
        Java                  :    42.26% ( 2506 Users)
        Bash/Shell/PowerShell :    40.76% ( 2417 Users)
        C++                   :    39.87% ( 2364 Users)
        C                     :    34.59% ( 2051 Users)
        PHP                   :    25.67% ( 1522 Users)
        C#                    :    24.28% ( 1440 Users)
        R                     :    19.73% ( 1170 Users)
        Other(s):             :    14.87% (  882 Users)
        TypeScript            :    14.17% (  840 Users)
        Assembly              :    12.58% (  746 Users)
        Go                    :     7.42% (  440 Users)
        Ruby                  :     6.83% (  405 Users)
        VBA                   :     6.22% (  369 Users)
        Swift                 :      5.4% (  320 Users)
        Kotlin                :     5.35% (  317 Users)
        Scala                 :     4.94% (  293 Users)
        Rust                  :      4.7% (  279 Users)
        Objective-C           :     4.37% (  259 Users)
        Dart                  :     2.02% (  120 Users)
        Clojure               :     2.02% (  120 Users)
        WebAssembly           :     1.87% (  111 Users)
        NA                    :     1.82% (  108 Users)
        Erlang                :     1.62% (   96 Users)
        Elixir                :     1.57% (   93 Users)
        F#                    :     1.45% (   86 Users)
Developer, mobile
        JavaScript            :    67.72% ( 9953 Users)
        HTML/CSS              :    62.46% ( 9181 Users)
        Java                  :    57.21% ( 8409 Users)
        SQL                   :    51.27% ( 7536 Users)
        C#                    :    34.34% ( 5048 Users)
        Python                :    31.88% ( 4685 Users)
        PHP                   :    30.71% ( 4514 Users)
        Bash/Shell/PowerShell :    29.49% ( 4334 Users)
        C++                   :    25.25% ( 3711 Users)
        Swift                 :    25.19% ( 3702 Users)
        TypeScript            :    25.03% ( 3679 Users)
        C                     :    22.81% ( 3352 Users)
        Kotlin                :    19.51% ( 2867 Users)
        Objective-C           :    18.73% ( 2753 Users)
        Ruby                  :     8.01% ( 1178 Users)
        Go                    :     6.93% ( 1018 Users)
        Assembly              :     6.79% (  998 Users)
        Other(s):             :     6.71% (  986 Users)
        Dart                  :      5.8% (  852 Users)
        VBA                   :     4.76% (  700 Users)
        R                     :     2.87% (  422 Users)
        Rust                  :      2.5% (  368 Users)
        Scala                 :     2.37% (  349 Users)
        WebAssembly           :     1.63% (  239 Users)
        Elixir                :     1.54% (  226 Users)
        F#                    :     1.22% (  179 Users)
        Clojure               :     1.15% (  169 Users)
        Erlang                :     0.87% (  128 Users)
        NA                    :     0.82% (  120 Users)
Data or business analyst
        SQL                   :    73.88% ( 4650 Users)
        HTML/CSS              :    62.11% ( 3909 Users)
        JavaScript            :    61.33% ( 3860 Users)
        Python                :    51.86% ( 3264 Users)
        Bash/Shell/PowerShell :    38.43% ( 2419 Users)
        Java                  :    33.97% ( 2138 Users)
        C#                    :    32.54% ( 2048 Users)
        PHP                   :    26.63% ( 1676 Users)
        R                     :    21.08% ( 1327 Users)
        C++                   :    19.35% ( 1218 Users)
        VBA                   :    17.59% ( 1107 Users)
        C                     :    17.13% ( 1078 Users)
        TypeScript            :    15.35% (  966 Users)
        Other(s):             :    11.93% (  751 Users)
        Go                    :      6.7% (  422 Users)
        Assembly              :     6.16% (  388 Users)
        Ruby                  :      6.1% (  384 Users)
        Scala                 :     4.81% (  303 Users)
        Swift                 :      4.5% (  283 Users)
        Objective-C           :     4.07% (  256 Users)
        Kotlin                :     3.65% (  230 Users)
        Rust                  :     1.97% (  124 Users)
        WebAssembly           :     1.75% (  110 Users)
        Clojure               :      1.6% (  101 Users)
        Dart                  :     1.56% (   98 Users)
        F#                    :     1.51% (   95 Users)
        Elixir                :     1.37% (   86 Users)
        NA                    :     1.33% (   84 Users)
        Erlang                :     1.19% (   75 Users)
Data scientist or machine learning specialist
        Python                :    79.33% ( 5125 Users)
        SQL                   :    58.44% ( 3775 Users)
        JavaScript            :    51.38% ( 3319 Users)
        HTML/CSS              :    50.43% ( 3258 Users)
        Bash/Shell/PowerShell :    44.49% ( 2874 Users)
        Java                  :    37.97% ( 2453 Users)
        C++                   :    31.98% ( 2066 Users)
        R                     :    30.57% ( 1975 Users)
        C                     :    25.91% ( 1674 Users)
        C#                    :    22.65% ( 1463 Users)
        PHP                   :    18.54% ( 1198 Users)
        TypeScript            :    13.25% (  856 Users)
        Other(s):             :    10.56% (  682 Users)
        Scala                 :     9.46% (  611 Users)
        Assembly              :     8.75% (  565 Users)
        Go                    :     8.72% (  563 Users)
        VBA                   :     7.59% (  490 Users)
        Ruby                  :     6.59% (  426 Users)
        Swift                 :     5.06% (  327 Users)
        Kotlin                :     4.71% (  304 Users)
        Objective-C           :     3.93% (  254 Users)
        Rust                  :     3.67% (  237 Users)
        Clojure               :     2.17% (  140 Users)
        WebAssembly           :     1.87% (  121 Users)
        Dart                  :     1.84% (  119 Users)
        Elixir                :     1.67% (  108 Users)
        F#                    :     1.55% (  100 Users)
        Erlang                :     1.47% (   95 Users)
        NA                    :     1.04% (   67 Users)
Database administrator
        SQL                   :     81.7% ( 7778 Users)
        JavaScript            :    78.11% ( 7436 Users)
        HTML/CSS              :    76.19% ( 7253 Users)
        Bash/Shell/PowerShell :     45.2% ( 4303 Users)
        PHP                   :    44.16% ( 4204 Users)
        Python                :    41.44% ( 3945 Users)
        C#                    :    40.18% ( 3825 Users)
        Java                  :    38.41% ( 3657 Users)
        C++                   :    22.37% ( 2130 Users)
        TypeScript            :    22.34% ( 2127 Users)
        C                     :    19.93% ( 1897 Users)
        Other(s):             :    11.66% ( 1110 Users)
        VBA                   :    11.31% ( 1077 Users)
        Go                    :    10.37% (  987 Users)
        Ruby                  :     9.02% (  859 Users)
        Assembly              :     7.48% (  712 Users)
        R                     :      6.1% (  581 Users)
        Swift                 :     5.83% (  555 Users)
        Kotlin                :     5.24% (  499 Users)
        Objective-C           :     4.85% (  462 Users)
        Scala                 :     3.33% (  317 Users)
        Rust                  :      3.2% (  305 Users)
        Dart                  :     2.24% (  213 Users)
        Elixir                :     2.08% (  198 Users)
        WebAssembly           :     1.91% (  182 Users)
        Erlang                :     1.54% (  147 Users)
        F#                    :     1.47% (  140 Users)
        Clojure               :     1.41% (  134 Users)
        NA                    :     0.85% (   81 Users)
Engineer, data
        SQL                   :    66.75% ( 3884 Users)
        Python                :    64.31% ( 3742 Users)
        JavaScript            :    60.13% ( 3499 Users)
        HTML/CSS              :    56.47% ( 3286 Users)
        Bash/Shell/PowerShell :    48.55% ( 2825 Users)
        Java                  :    42.69% ( 2484 Users)
        C++                   :    27.69% ( 1611 Users)
        C#                    :    27.07% ( 1575 Users)
        C                     :    25.04% ( 1457 Users)
        PHP                   :    24.08% ( 1401 Users)
        TypeScript            :    16.09% (  936 Users)
        R                     :     14.8% (  861 Users)
        Scala                 :     12.8% (  745 Users)
        Go                    :     11.7% (  681 Users)
        Other(s):             :     11.1% (  646 Users)
        VBA                   :     9.06% (  527 Users)
        Assembly              :     8.94% (  520 Users)
        Ruby                  :     8.87% (  516 Users)
        Kotlin                :     5.16% (  300 Users)
        Swift                 :     5.12% (  298 Users)
        Objective-C           :     4.33% (  252 Users)
        Rust                  :     4.07% (  237 Users)
        Clojure               :     2.37% (  138 Users)
        Elixir                :     2.11% (  123 Users)
        Dart                  :     1.86% (  108 Users)
        Erlang                :      1.8% (  105 Users)
        WebAssembly           :     1.77% (  103 Users)
        F#                    :     1.63% (   95 Users)
        NA                    :     1.05% (   61 Users)
Engineer, site reliability
        JavaScript            :    69.43% ( 2049 Users)
        Bash/Shell/PowerShell :    64.05% ( 1890 Users)
        HTML/CSS              :    62.79% ( 1853 Users)
        SQL                   :    61.37% ( 1811 Users)
        Python                :    59.23% ( 1748 Users)
        Java                  :     40.6% ( 1198 Users)
        PHP                   :     30.9% (  912 Users)
        Go                    :    30.57% (  902 Users)
        C#                    :    24.09% (  711 Users)
        TypeScript            :    22.06% (  651 Users)
        C                     :    21.92% (  647 Users)
        C++                   :    21.65% (  639 Users)
        Ruby                  :    19.76% (  583 Users)
        Other(s):             :    11.72% (  346 Users)
        Assembly              :     8.71% (  257 Users)
        Scala                 :     7.35% (  217 Users)
        Kotlin                :     7.25% (  214 Users)
        Rust                  :     6.74% (  199 Users)
        Swift                 :     6.44% (  190 Users)
        VBA                   :     5.29% (  156 Users)
        R                     :     5.25% (  155 Users)
        Objective-C           :     4.68% (  138 Users)
        Elixir                :     4.61% (  136 Users)
        Erlang                :     4.17% (  123 Users)
        Clojure               :     3.66% (  108 Users)
        WebAssembly           :     2.78% (   82 Users)
        Dart                  :     2.27% (   67 Users)
        F#                    :     2.13% (   63 Users)
        NA                    :     1.19% (   35 Users)
Developer, QA or test
        JavaScript            :    73.38% ( 4666 Users)
        HTML/CSS              :    70.31% ( 4471 Users)
        SQL                   :    64.81% ( 4121 Users)
        Bash/Shell/PowerShell :    45.73% ( 2908 Users)
        Java                  :    45.23% ( 2876 Users)
        Python                :    42.08% ( 2676 Users)
        C#                    :    37.47% ( 2383 Users)
        PHP                   :    33.23% ( 2113 Users)
        C++                   :    25.07% ( 1594 Users)
        TypeScript            :    23.59% ( 1500 Users)
        C                     :    22.39% ( 1424 Users)
        Ruby                  :    11.06% (  703 Users)
        Other(s):             :    10.96% (  697 Users)
        Go                    :     9.73% (  619 Users)
        VBA                   :     8.26% (  525 Users)
        Assembly              :     7.67% (  488 Users)
        Swift                 :      7.6% (  483 Users)
        Kotlin                :     6.81% (  433 Users)
        Objective-C           :      6.6% (  420 Users)
        R                     :      4.4% (  280 Users)
        Rust                  :     3.55% (  226 Users)
        Scala                 :     3.52% (  224 Users)
        Dart                  :     2.33% (  148 Users)
        WebAssembly           :     2.01% (  128 Users)
        F#                    :     1.97% (  125 Users)
        Elixir                :     1.86% (  118 Users)
        Clojure               :     1.65% (  105 Users)
        Erlang                :     1.43% (   91 Users)
        NA                    :     0.93% (   59 Users)
DevOps specialist
        JavaScript            :    73.67% ( 6529 Users)
        HTML/CSS              :    66.66% ( 5907 Users)
        SQL                   :    64.56% ( 5721 Users)
        Bash/Shell/PowerShell :    63.98% ( 5670 Users)
        Python                :    52.44% ( 4647 Users)
        Java                  :     41.2% ( 3651 Users)
        C#                    :    32.79% ( 2906 Users)
        PHP                   :    28.85% ( 2557 Users)
        TypeScript            :     28.2% ( 2499 Users)
        Go                    :     20.1% ( 1781 Users)
        C++                   :    18.84% ( 1670 Users)
        C                     :    18.21% ( 1614 Users)
        Ruby                  :    14.82% ( 1313 Users)
        Other(s):             :     9.78% (  867 Users)
        Kotlin                :     6.93% (  614 Users)
        Scala                 :     6.03% (  534 Users)
        Assembly              :     5.83% (  517 Users)
        Swift                 :     5.33% (  472 Users)
        Rust                  :     5.17% (  458 Users)
        VBA                   :      4.8% (  425 Users)
        R                     :     4.55% (  403 Users)
        Objective-C           :     4.52% (  401 Users)
        Elixir                :     2.97% (  263 Users)
        Clojure               :     2.23% (  198 Users)
        Erlang                :     2.18% (  193 Users)
        WebAssembly           :     2.11% (  187 Users)
        F#                    :     1.97% (  175 Users)
        Dart                  :     1.94% (  172 Users)
        NA                    :     0.56% (   50 Users)
Developer, game or graphics
        JavaScript            :    69.02% ( 3064 Users)
        HTML/CSS              :    66.37% ( 2946 Users)
        C#                    :    54.31% ( 2411 Users)
        SQL                   :    48.91% ( 2171 Users)
        C++                   :    47.85% ( 2124 Users)
        Java                  :    45.33% ( 2012 Users)
        Python                :    44.22% ( 1963 Users)
        Bash/Shell/PowerShell :    37.46% ( 1663 Users)
        C                     :    32.69% ( 1451 Users)
        PHP                   :    31.83% ( 1413 Users)
        TypeScript            :    22.37% (  993 Users)
        Assembly              :    12.84% (  570 Users)
        Other(s):             :    11.98% (  532 Users)
        Objective-C           :    10.95% (  486 Users)
        Swift                 :    10.48% (  465 Users)
        Go                    :     8.65% (  384 Users)
        Kotlin                :     8.38% (  372 Users)
        Ruby                  :     8.06% (  358 Users)
        Rust                  :     6.71% (  298 Users)
        VBA                   :     6.38% (  283 Users)
        R                     :     3.94% (  175 Users)
        WebAssembly           :     3.65% (  162 Users)
        Dart                  :      3.2% (  142 Users)
        Scala                 :     2.93% (  130 Users)
        F#                    :     2.19% (   97 Users)
        Elixir                :     1.89% (   84 Users)
        Clojure               :     1.67% (   74 Users)
        Erlang                :      1.4% (   62 Users)
        NA                    :     0.92% (   41 Users)
Educator
        JavaScript            :    70.15% ( 3151 Users)
        HTML/CSS              :    70.15% ( 3151 Users)
        SQL                   :    56.92% ( 2557 Users)
        Python                :    47.02% ( 2112 Users)
        Java                  :    44.26% ( 1988 Users)
        Bash/Shell/PowerShell :    40.89% ( 1837 Users)
        PHP                   :    34.04% ( 1529 Users)
        C#                    :    30.21% ( 1357 Users)
        C++                   :    28.56% ( 1283 Users)
        C                     :    26.91% ( 1209 Users)
        TypeScript            :    21.39% (  961 Users)
        Other(s):             :    13.31% (  598 Users)
        R                     :     10.6% (  476 Users)
        Ruby                  :    10.13% (  455 Users)
        Assembly              :     9.95% (  447 Users)
        Go                    :     7.59% (  341 Users)
        VBA                   :     7.48% (  336 Users)
        Kotlin                :     7.39% (  332 Users)
        Swift                 :     7.26% (  326 Users)
        Objective-C           :     5.54% (  249 Users)
        Scala                 :     4.36% (  196 Users)
        Rust                  :     4.01% (  180 Users)
        Dart                  :     2.94% (  132 Users)
        Elixir                :     2.27% (  102 Users)
        WebAssembly           :     2.14% (   96 Users)
        Clojure               :     2.07% (   93 Users)
        F#                    :     1.98% (   89 Users)
        Erlang                :     1.76% (   79 Users)
        NA                    :     1.18% (   53 Users)
Student
        HTML/CSS              :    68.13% ( 8122 Users)
        JavaScript            :    63.53% ( 7574 Users)
        Java                  :    54.37% ( 6482 Users)
        Python                :    54.37% ( 6481 Users)
        SQL                   :    51.83% ( 6179 Users)
        C++                   :    39.59% ( 4720 Users)
        C                     :    37.91% ( 4519 Users)
        Bash/Shell/PowerShell :    33.97% ( 4050 Users)
        PHP                   :    31.33% ( 3735 Users)
        C#                    :    30.19% ( 3599 Users)
        TypeScript            :    15.84% ( 1888 Users)
        Assembly              :    14.65% ( 1747 Users)
        R                     :     9.23% ( 1100 Users)
        Other(s):             :     8.51% ( 1015 Users)
        Kotlin                :     6.97% (  831 Users)
        Ruby                  :     6.45% (  769 Users)
        Swift                 :     6.32% (  754 Users)
        Go                    :     6.21% (  740 Users)
        VBA                   :     5.15% (  614 Users)
        Rust                  :     4.38% (  522 Users)
        Objective-C           :     3.53% (  421 Users)
        Dart                  :     2.94% (  351 Users)
        Scala                 :     2.84% (  339 Users)
        NA                    :     1.93% (  230 Users)
        WebAssembly           :     1.39% (  166 Users)
        F#                    :     1.28% (  152 Users)
        Clojure               :     1.12% (  133 Users)
        Elixir                :      1.1% (  131 Users)
        Erlang                :      0.9% (  107 Users)
Engineering manager
        JavaScript            :    72.35% ( 3040 Users)
        HTML/CSS              :    65.02% ( 2732 Users)
        SQL                   :     60.4% ( 2538 Users)
        Bash/Shell/PowerShell :     49.1% ( 2063 Users)
        Python                :    46.86% ( 1969 Users)
        Java                  :    39.81% ( 1673 Users)
        C#                    :    31.15% ( 1309 Users)
        PHP                   :    25.99% ( 1092 Users)
        TypeScript            :    25.46% ( 1070 Users)
        C++                   :    23.01% (  967 Users)
        C                     :    21.42% (  900 Users)
        Go                    :    15.42% (  648 Users)
        Ruby                  :    14.97% (  629 Users)
        Other(s):             :      9.9% (  416 Users)
        Swift                 :     9.85% (  414 Users)
        Objective-C           :     8.54% (  359 Users)
        Assembly              :     8.09% (  340 Users)
        Kotlin                :     7.92% (  333 Users)
        Scala                 :     6.31% (  265 Users)
        VBA                   :     6.24% (  262 Users)
        R                     :     5.93% (  249 Users)
        Rust                  :     4.57% (  192 Users)
        Elixir                :      3.4% (  143 Users)
        Clojure               :     2.76% (  116 Users)
        Dart                  :     2.45% (  103 Users)
        F#                    :     2.33% (   98 Users)
        Erlang                :     2.31% (   97 Users)
        WebAssembly           :     2.17% (   91 Users)
        NA                    :     0.93% (   39 Users)
Senior executive/VP
        JavaScript            :    75.94% ( 1600 Users)
        HTML/CSS              :    71.81% ( 1513 Users)
        SQL                   :    64.12% ( 1351 Users)
        Bash/Shell/PowerShell :     46.8% (  986 Users)
        Python                :    46.37% (  977 Users)
        Java                  :    36.36% (  766 Users)
        PHP                   :    34.79% (  733 Users)
        C#                    :    32.37% (  682 Users)
        TypeScript            :    26.48% (  558 Users)
        C++                   :    23.49% (  495 Users)
        C                     :    22.21% (  468 Users)
        Ruby                  :    14.86% (  313 Users)
        Go                    :    14.14% (  298 Users)
        Swift                 :    12.43% (  262 Users)
        Other(s):             :    11.77% (  248 Users)
        Objective-C           :    10.82% (  228 Users)
        Assembly              :    10.11% (  213 Users)
        VBA                   :     7.93% (  167 Users)
        Kotlin                :     7.69% (  162 Users)
        R                     :     7.31% (  154 Users)
        Scala                 :     6.26% (  132 Users)
        Rust                  :     5.55% (  117 Users)
        Elixir                :     4.27% (   90 Users)
        WebAssembly           :     4.18% (   88 Users)
        Clojure               :     4.08% (   86 Users)
        Dart                  :     3.99% (   84 Users)
        Erlang                :     2.94% (   62 Users)
        F#                    :     2.52% (   53 Users)
        NA                    :     1.57% (   33 Users)
System administrator
        JavaScript            :    73.45% ( 6558 Users)
        HTML/CSS              :    72.57% ( 6480 Users)
        SQL                   :    67.94% ( 6066 Users)
        Bash/Shell/PowerShell :    58.44% ( 5218 Users)
        Python                :    51.36% ( 4586 Users)
        PHP                   :    43.01% ( 3840 Users)
        Java                  :    39.02% ( 3484 Users)
        C#                    :    31.08% ( 2775 Users)
        C++                   :    24.86% ( 2220 Users)
        C                     :    24.64% ( 2200 Users)
        TypeScript            :    19.08% ( 1704 Users)
        Go                    :    13.93% ( 1244 Users)
        Other(s):             :     12.5% ( 1116 Users)
        Ruby                  :    12.08% ( 1079 Users)
        VBA                   :     9.33% (  833 Users)
        Assembly              :     8.89% (  794 Users)
        Swift                 :      6.0% (  536 Users)
        Kotlin                :     5.59% (  499 Users)
        R                     :      5.4% (  482 Users)
        Objective-C           :     4.71% (  421 Users)
        Rust                  :     4.69% (  419 Users)
        Scala                 :     3.29% (  294 Users)
        Dart                  :     2.27% (  203 Users)
        Elixir                :     2.25% (  201 Users)
        WebAssembly           :     2.14% (  191 Users)
        Clojure               :     1.92% (  171 Users)
        Erlang                :     1.87% (  167 Users)
        F#                    :     1.25% (  112 Users)
        NA                    :     0.82% (   73 Users)
Developer, embedded applications or devices
        JavaScript            :    60.89% ( 4413 Users)
        HTML/CSS              :    57.75% ( 4186 Users)
        C++                   :    51.08% ( 3702 Users)
        SQL                   :    50.97% ( 3694 Users)
        Python                :    50.95% ( 3693 Users)
        C                     :    49.99% ( 3623 Users)
        Bash/Shell/PowerShell :    47.35% ( 3432 Users)
        Java                  :    44.25% ( 3207 Users)
        C#                    :    39.45% ( 2859 Users)
        PHP                   :    27.84% ( 2018 Users)
        TypeScript            :    19.12% ( 1386 Users)
        Assembly              :    17.92% ( 1299 Users)
        Other(s):             :    12.17% (  882 Users)
        Go                    :    10.18% (  738 Users)
        Swift                 :     9.73% (  705 Users)
        Objective-C           :     8.91% (  646 Users)
        Kotlin                :     8.07% (  585 Users)
        VBA                   :      7.7% (  558 Users)
        Ruby                  :     7.13% (  517 Users)
        Rust                  :     6.39% (  463 Users)
        R                     :      4.3% (  312 Users)
        Dart                  :     3.26% (  236 Users)
        Scala                 :     2.94% (  213 Users)
        WebAssembly           :     2.77% (  201 Users)
        F#                    :      1.9% (  138 Users)
        Erlang                :     1.74% (  126 Users)
        Elixir                :     1.66% (  120 Users)
        Clojure               :     1.38% (  100 Users)
        NA                    :     0.87% (   63 Users)
Product manager
        JavaScript            :     75.0% ( 3024 Users)
        HTML/CSS              :    71.92% ( 2900 Users)
        SQL                   :    63.42% ( 2557 Users)
        Python                :    39.63% ( 1598 Users)
        Bash/Shell/PowerShell :    38.96% ( 1571 Users)
        PHP                   :    36.16% ( 1458 Users)
        Java                  :    35.44% ( 1429 Users)
        C#                    :    33.85% ( 1365 Users)
        TypeScript            :     25.2% ( 1016 Users)
        C++                   :    22.17% (  894 Users)
        C                     :    19.15% (  772 Users)
        Swift                 :    10.94% (  441 Users)
        Ruby                  :    10.54% (  425 Users)
        Other(s):             :     9.95% (  401 Users)
        Go                    :     9.65% (  389 Users)
        VBA                   :     8.31% (  335 Users)
        Objective-C           :     8.18% (  330 Users)
        Assembly              :     6.94% (  280 Users)
        Kotlin                :     6.72% (  271 Users)
        R                     :      5.8% (  234 Users)
        Rust                  :     3.45% (  139 Users)
        Dart                  :      3.4% (  137 Users)
        Scala                 :     3.27% (  132 Users)
        Elixir                :     2.43% (   98 Users)
        Clojure               :     2.18% (   88 Users)
        WebAssembly           :     2.08% (   84 Users)
        F#                    :     1.79% (   72 Users)
        Erlang                :     1.79% (   72 Users)
        NA                    :     1.41% (   57 Users)
Scientist
        Python                :    69.48% ( 2513 Users)
        HTML/CSS              :    51.04% ( 1846 Users)
        JavaScript            :    48.77% ( 1764 Users)
        Bash/Shell/PowerShell :    47.83% ( 1730 Users)
        SQL                   :    44.21% ( 1599 Users)
        C++                   :    41.36% ( 1496 Users)
        Java                  :    34.89% ( 1262 Users)
        C                     :    34.01% ( 1230 Users)
        R                     :    25.82% (  934 Users)
        C#                    :    21.68% (  784 Users)
        PHP                   :     20.6% (  745 Users)
        Other(s):             :    18.36% (  664 Users)
        Assembly              :    12.36% (  447 Users)
        TypeScript            :    11.75% (  425 Users)
        Go                    :     8.24% (  298 Users)
        VBA                   :     7.77% (  281 Users)
        Ruby                  :     6.64% (  240 Users)
        Scala                 :     6.05% (  219 Users)
        Swift                 :     5.53% (  200 Users)
        Rust                  :     5.42% (  196 Users)
        Kotlin                :     5.11% (  185 Users)
        Objective-C           :     4.92% (  178 Users)
        WebAssembly           :     2.27% (   82 Users)
        Clojure               :     2.21% (   80 Users)
        F#                    :     2.07% (   75 Users)
        Dart                  :     1.82% (   66 Users)
        Erlang                :     1.66% (   60 Users)
        Elixir                :     1.58% (   57 Users)
        NA                    :     1.08% (   39 Users)
Marketing or sales professional
        HTML/CSS              :    76.82% (  749 Users)
        JavaScript            :    71.79% (  700 Users)
        SQL                   :    58.97% (  575 Users)
        PHP                   :    44.21% (  431 Users)
        Python                :    38.26% (  373 Users)
        Java                  :    33.03% (  322 Users)
        Bash/Shell/PowerShell :     32.1% (  313 Users)
        C#                    :     24.1% (  235 Users)
        C++                   :    19.49% (  190 Users)
        C                     :    17.44% (  170 Users)
        TypeScript            :    16.62% (  162 Users)
        VBA                   :    13.44% (  131 Users)
        Other(s):             :    13.13% (  128 Users)
        Ruby                  :    12.21% (  119 Users)
        Assembly              :    11.49% (  112 Users)
        Swift                 :    10.67% (  104 Users)
        R                     :     9.44% (   92 Users)
        Go                    :     8.51% (   83 Users)
        Objective-C           :     8.21% (   80 Users)
        Kotlin                :     6.05% (   59 Users)
        Scala                 :     4.82% (   47 Users)
        WebAssembly           :     4.51% (   44 Users)
        NA                    :     4.31% (   42 Users)
        Dart                  :     4.21% (   41 Users)
        Rust                  :     3.79% (   37 Users)
        F#                    :     3.69% (   36 Users)
        Elixir                :     3.49% (   34 Users)
        Clojure               :     3.49% (   34 Users)
        Erlang                :     2.97% (   29 Users)
```
</details>





<!-- <details>
<summary>
<h5>
    Q: xxx?
</h5>
</summary>

> CHANGES: xxx?

``` py
```
```
```
</details> -->

<!-- <details>
<summary> v1.0 </summary>

> CHANGES: Check for entries.

``` py
```
```
```
</details> -->
