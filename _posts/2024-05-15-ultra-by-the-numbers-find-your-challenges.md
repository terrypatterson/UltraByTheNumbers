---
title: Find Your Challenges Before Rolling Out Ultra
date: 2024-07-11 12:00:00 -0500
categories: [Ultra Migration, Challenges, SQL]
tags: [SQL, Ultra, Blackboard]
---

# Find Your Challenges Before Rolling Out Ultra

So you've decided to migration to Ultra Course View. Change is never an easy task, in fact its one of the most challenging things anyone can do. 

## Ultra Readiness

Anthology has a tool kit which is free to institutions planning to migrate to Ultra. It has some very good resources which we will discuss. More information on this tool kit can be found at this link, [https://learn-toolkit.anthology.com/](https://learn-toolkit.anthology.com/)

## Utilized Tools Status


## Folder Depth

The move to Ultra Course view requires some courses which have many nested folders to be flattened. By default, Ultra sets a max of two folders deep, but can be increased to 3. This is a permanent change that can't be reverted so it's important to understand the impact of this change to courses. Mike Buchanon created a great SQL script that can gather which courses would be impacted. It's shown below.

```

{

-- would there be a way to count the folder depth in use on Original Courses from DDA?
-- Mike Buchanan
--identify possibly problematic folder depth in Original courses
WITH RECURSIVE cte (crsmain_pk1, pk1, title, path, parent_pk1, depth)  AS (
    SELECT  crsmain_pk1,
        pk1,
        title,
        '' || title AS path,
        parent_pk1,
        1 AS depth
    FROM course_contents
    WHERE parent_pk1 IS NULL and cnthndlr_handle='resource/x-bb-folder'
    UNION ALL
    SELECT course_contents.crsmain_pk1,
        course_contents.pk1,
        course_contents.title,
        cte.path || ' > ' || course_contents.title as path,
        course_contents.parent_pk1,
        cte.depth + 1 AS depth
    FROM course_contents
    JOIN cte
        ON course_contents.parent_pk1 = cte.pk1
    where course_contents.cnthndlr_handle = 'resource/x-bb-folder'
)
SELECT cm.course_id, cte.path, cte.depth
FROM cte
join course_main cm on cm.pk1 = cte.crsmain_pk1
where cm.course_id like '22%'
-- adjust based on 2 or 3 depth level in Ultra courses, depending on your settings
and cte.depth > 3
and cm.ultra_status = 'C'
order by cm.course_id, cte.path`

}

```


## Illuminate Reports


## Ultra Tranition Toolkit Reports


## Plan for Actions

