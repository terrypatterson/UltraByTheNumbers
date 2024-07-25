---
title: Where to Go From Here
date: 2024-07-11 12:00:00 -0500
categories: [Ultra Migration, SQL]
tags: [SQL, Ultra, Blackboard]
---

# Where to Go From Here

Once an institution understands where they are regarding a move to the Ultra Course View, it needs to focus on four key areas that will help with change management process.

## Phased vs Cutover

Institutions can take one of two steps to move Blackboard courses onto the Ultra experience. One is a phased approach, moving content over by department, division, or by delivery method. Another approach is to migrate all Blackboard courses to the Ultra experience in a single term. This is commonly called a cutover approach. Here are the pros and cons of both options.

<table width="90%">
<th colspan="2">Phased</th>
<tr><td>Allows for comparative delivery analysis</td><td>Multiple course experiences could cause confusion for students</td></tr>
<tr><td>Ultra champions / instructors to fully experience UCV and share feedback to others</td><td>Instructors must retain workflows for both course views during transition</td></tr>
<tr><td>Increases knowledge and expertise in teaching / using Ultra Course View</td><td>Staff must support both instructors and students using both experiences</td></tr>
</table>

<br />
<br />

<table width="90%">
<th colspan="2">Cutover</th>
<tr><td>Clear delineation between student / instructor experiences</td><td>Requires everyone to be prepared for new course view / experience</td></tr>
<tr><td>Removes duplication of supporting two course experiences for instructors and students</td><td>Inability to confirm and/or test changes with students to ensure success</td></tr>
<tr><td>Allows separation of development for Ultra courses versus current course delivery</td><td>Communication and change management important to the success of this process</td></tr>
</table>



## Course Development

When moving to Ultra Course view, an institution can take many different approaches. These fall into normally three different categories - 

#### Developmental Course Shells - The institution creates course shells for instructors to develop new course materials in the Ultra Course view. Normally these should be available for a limited time during the migration from Original to Ultra.

#### Utilize Current Course Shells - The institution creates course shells that will be used for instruction and allows development of Ultra Course content before, during, or after instruction

#### Course Template Structure - The institution creates Ultra course templates for courses which will then be copied into instructional course shells.

## Instructor Activity Measurements

While monitoring specific instructors might create some privacy concerns at intitutions, understanding who is working in Ultra courses can provide great insight on who your early adopters and Ultra "champions" can be within a department, college, or your entire institution.

Generalized data about instructor interactions can be helpful just to understand what communication and training offerings have the greatest impact to engage instructors with Ultra courses.

While we always want to try to use the "carrot" approach when pushing adoption. Institutions may have need to report to leadership users and/or departments failing to meet adoption deadlines for a successful roll-out.

The code below will allow you to find the most active users within a specific set of courses.

```
select u.user_id as "Username",
	   string_agg(distinct u.firstname||' '||u.lastname, ', ') as "User",
	   COUNT(distinct aa.session_id) as "Sessions",
	   COUNT(aa.pk1) as "Events"
from activity_accumulator aa
	join users u
	 on aa.user_pk1 = u.pk1
	join course_main cm
	 on aa.course_pk1 = cm.pk1
where cm.course_id like '%UBO%'
  and u.user_id not like '%_PreviewUser'
  and u.user_id not in ('admin_user1','admin_user2','admin_user3')
group by "Username"
order by "Sessions" desc;
```

Here's a sample of the results you will get from the query above.

![image of a list of names](assets/img/posts/ultra-pres/champion-list.png)

## Implementation by Department

Similar to the previous topic discussed. Department monitoring offers valuable information about training successes and gaps, departments leading the migration to Ultra, and identify departments lagging in their Ultra adoption processes.

Here's a bar graph broken down by department.

![a bar graph broken down by departments](assets/img/posts/ultra-pres/department_monitoring.png)

