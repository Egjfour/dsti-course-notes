|         Course Name         |       Topic        | Professor |     Date      |         Tags         |
| :-------------------------: | :----------------: | :-------: | :-----------: | :------------------: |
| **Intro - Data Management** | Relational Algebra | Sebastien | 18 April 2024 | #SQL#Data_Management |

[Moodle Link](https://learn.dsti.institute/pluginfile.php/28088/mod_resource/content/0/Relational-Model-Worksheet.pdf)

![[Pasted image 20240418165135.png]]

**ATTEMPTED ANSWERS:**
*Question 1*

$$
\displaylines{
T1 = \sigma Movie(Country == 'France')\\
T2 = \pi T1(title, director, year)
}
$$

*Question 2*
$$
\displaylines{
T1 = \sigma \:Program(CinemaName == 'Pathé \:Masséna'\: AND\: Week = WEEK(TODAY()))\\
T2 = \pi \:T1(Title)
}
$$

*Question 3*
$$
\displaylines{
T1 = \sigma \: Distribution(Title == 'Inception')\\
T2 = \pi T1(ActorName)
}
$$

*Question 4*
$$
\displaylines{
T1 = \sigma Program(Title == 'Midnight\:In\:Paris')\\
T2 = \pi T1(CinemaName, ScreenNumber)\\
T3 = \pi Screen(CinemaName, ScreenNumber, SeatNumber)\\
T4 = T3 \Join T2
}
$$

*Question 5*
$$
\displaylines{
T1 = \sigma Movie(Director == 'Scorscese')\\
T2 = \pi T1(Title)\\
T3 = \pi Program(CinemaName, Title)\\
T4 = T2 \Join T3\\
T5 = \pi Cinema(CinemaName, Street)\\
T6 = T4 \Join T5\\
T7 = \pi T6(Street)
}
$$

*Question 6*
$$
\displaylines{
T1 = \sigma Distribution(ActorName == 'Angelina\: Jolie')\\
T2 = \sigma Distribution(ActorName == 'Matt\: Damon')\\
T3 = T1 \:\cup\: T2\\
T4 = \pi T3(Title)\\
T5 = \pi Program(CinemaName, Title)\\
T6 = T4 \Join T5\\
T7 = \pi Cinema(CinemaName, Street)\\
T8 = T6 \Join T7\\
T9 = \pi T8(Street)
}
$$

*Question 7*
$$
\displaylines{
T1 = \sigma Distribution(ActorName == 'Angelina\: Jolie')\\
T2 = \sigma Distribution(ActorName == 'Johnny\: Depp')\\
T3 = \pi T1(Title)\\
T4 = \pi T2(Title)\\
T5 = T3 \Join T4\\
T6 = \pi Program(CinemaName, Title)\\
T7 = T5 \Join T6\\
T8 = \pi Cinema(CinemaName, Street)\\
T9 = T7 \Join T8\\
T10 = \pi T9(Street)
}
$$

*Question 8*
$$
\displaylines{
T1 = \sigma Distribution(ActorName == 'Leonardo\: DiCaprio')\\
T2 = \pi T1(Title)\\
T3 = \sigma Program(Year = YEAR(Week))\\
T4 = T2 \Join T3\\
T5 = \pi T4(Year)
}
$$

*Question 9*
$$
\displaylines{
T1 = \sigma Movie(Director == 'James \:Cameron')\\
T2 = \pi T1(Title)\\
T3 = \sigma Distribution(Title, ActorName)\\
T4 = T2 \Join T3\\
T5 = \sigma T4(ActorName)
}
$$

*Question 10*
$$
\displaylines{
T1 = \sigma Distribution(ActorName == 'Daniel \: Radcliffe')\\
T2 = \pi T1(Title)\\
T3 = \pi Distribution(Title, ActorName)\\
T4 = T2 \Join T3\\
T5 = \sigma T4(ActorName <> 'Daniel \:Radcliffe')
T6 = \pi T5(ActorName)
}
$$

*Question 11*
$$
\displaylines{
T1 = \sigma Movie(Director == 'Besson')\\
T2 = \pi T1(Title)\\
T3 = \sigma Distribution(Title, ActorName)\\
T4 = T2 \Join T3\\
T5 = \sigma T4(ActorName)
}
$$
*Question 12*
$$
\displaylines{
T1 = \sigma Movie(Year == 2010)\\
T2 = \pi T1(Title)\\
T3 = \sigma Distribution(ActorName == 'Brad \: Pitt')\\
T4 = \pi T3(Title)\\
T5 = T2 \Join T3\\
T6 = \pi Distribution(CinemaName, ScreenNumber, Title)\\
T7 = T5 \Join T6\\
T8 = \pi T7(CinemaName, ScreenNumber)\\
T9 \pi Cinema(CinemaName, Street)\\
T10 = \pi Screen(CinemaName, ScreenNumber, SeatNumber)\\
T11 = T8 \Join T9\\
T12 = T11 \Join T10\\
T13 = \pi T12(Street, ScreenNumber, SeatNumber)
}
$$

*Question 13*
$$
\displaylines{
T1 = \pi Movie(Title, Director)\\
T2 = \pi Distribution(ActorName)\\
T3 = T1 \underset{Director == ActorName \:AND\: Title}{\bowtie} T2\\
T4 = \pi T3(Title)
}
$$
