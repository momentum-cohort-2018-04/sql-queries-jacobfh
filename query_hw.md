<!-- Find all time entries -->

SELECT *
FROM time_entries;

<!-- Find the developer who joined most recently -->

SELECT MAX(created_at),*
FROM time_entries;

<!-- Find the number of projects for each client -->

SELECT client_id, COUNT(*) AS project_count
FROM projects
GROUP BY client_id;

<!-- Find all time entries, and show each one's client name next to it -->

SELECT *
FROM time_entries JOIN projects
ON time_entries.project_id = projects.id;

<!-- Find all developers in the "Ohio sheep" group -->

SELECT developers.name, group_id
FROM developers
JOIN group_assignments
ON group_assignments.developer_id = developers.id
WHERE group_id = 3;

<!-- Find the total number of hours worked for each client -->

SELECT project_id, SUM(duration) AS total_hours
FROM time_entries
GROUP BY project_id;

<!-- Find the client for whom Mrs. Lupe Schowalter (the developer) has worked the greatest number of hours -->

SELECT developer_id, project_id, SUM(duration) AS hours_worked, name
FROM time_entries
JOIN projects ON projects.id = time_entries.project_id
WHERE developer_id = 28
GROUP BY project_id 
ORDER BY duration DESC 
LIMIT 1;

<!-- List all client names with their project names (multiple rows for one client is fine).  Make sure that clients still show up even if they have no projects -->

SELECT projects.name AS project_name, clients.name AS client_name
FROM projects
JOIN clients ON clients.id = projects.client_id;

<!-- Find all developers who have written no comments -->

SELECT developers.name, comments.comment
FROM developers
LEFT JOIN comments
ON comments.developer_id = developers.id
Where comment IS null



