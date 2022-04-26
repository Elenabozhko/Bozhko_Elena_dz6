# Bozhko_Elena_dz6
Домашнее задание MYSQL6
-- Пусть задан некоторый пользователь. Из всех пользователей соц. сети найдите человека, 
	 который больше всех общался с выбранным пользователем (написал ему сообщений).---

select u.firstname, u.lastname
from users u 
join
messages m 
where m.from_user_id = u.id and m.to_user_id = 1
group by u.firstname, u.lastname 
order by count(from_user_id) desc 
limit 1

-- Подсчитать общее количество лайков, которые получили пользователи младше 10 лет..---

select count(*) 'likes count'
from likes l 
join
profiles p 
where p.user_id = l.user_id and timestampdiff(year, p.birtday, now()) <10
;

	 
	 
-- Определить кто больше поставил лайков (всего): мужчины или женщины.---

select case (gender)
	when 'm' then 'мужчин'
	when 'f' then 'женщин'
	end as 'Кого больше', COUNT(*) as 'лайков'
from profiles p 
join
likes l 
where l.user_id = p.user_id 
group by gender 
limit 1
