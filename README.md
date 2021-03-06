# Открытый голос/Openvoice

Блокчеин сеть для проведения открытых голосований, а так-же сопровождения договоров доверия.

## Сущности

name|название|описание
--------|-------|-------
account|учётная запись|Учётная запись. Текстовое поле data в учётной записи может содержать всю необходимую для идентификации пользователя информацию. Например никнейм или адрес или ФИО+часть СНИЛС. Подтверждение соответствия данных учётной записи и её владельца выполняется сторонними механизмами
admin|администратор|Учётная запись с правами управления какойлибо сущностью: группа, голосование, договор
group|группа|Сущность объединяющая аккаунты. Группа может быть открытая - любой пользователь может присоединиться, или закрытая - владелец/администратор подтверждает присоединение
owner|владелец|Учётная запись от имени которой создана сущность: группа, голосование, договор
trast_contract|договор|Договор одной стороной которого является владелец, второй присоединившиеся учётные записи (их владельцы), в т.ч. администраторы. Может быть публичный и приватный. К публичному может присоединиться любой пользователь, к приватному только после подтверждения владельца/администратора
vote|голосование|Сущность содержащая описание, варианты ответа, период и список групп, участники которых могут принять участие
user|пользователь|Человек пользующийся системой, может иметь неограниченное количество аккаунтов
miner|майнер|узел подписывающий очередной пакет
## Сценарии использования

### Регистрация

### Работа с группой

### Голосование открытое

### Голосование тайное

1) администратор создаёт голосование, указывает тип тайное, указывая, какие группы могут в нём участвовать
2) пользователь получает приглашение, на свой аккаунт зарегистированный в группе
3) пользователь голосует:
  1) создаётся временный анонимный аккаунт в котором есть имя
  TODO придумать, как реализовать тайное голосование, для гарантированного списка пользователей публично участвующих в группе

### Работа с Договором доверия

Исходные данные: есть небольшой посёлок. В сети Openvoice создана группа в которую входят все жители посёлка. В посёлке есть "Совет жителей". Каждый участник совета является постоянным представителем группы жителей. Этот факт подтверждается наличием Договора в Openvoice, владельцем поторого является участник совета. Форма договора у всех одинаковая
Допустим житель посёлка решил стать участником совета. Создовая договор он становится его владельцем.

#### Регистрация договора

№|исполнитель|действие|результат|
-|-----------|--------|---------|
1|Владалец|Создаёт договор, указывает группу, указывает что договор приватный, отправляет|В блок попадает запись о создании договора
2|Майнер|Подписывает пакет, в котором находится договор|Подписанный пакет попадает в блокчейн

#### Присоединение к договору

№|исполнитель|действие|результат|
-|-----------|--------|---------|
1|Пользователь|Создаёт запись, от имени аккаунта входящего в нужную группу, о желании присоединиться к договору - подпись
2|Майнер|Подписывает пакет, в котором находится запись|Заявка на присоединение к договору опубликована
3|Владелец/Администратор|Создаёт запись подтверждающую, что пользователь присоединился к договору
4|Майнер|Подписывает пакет, в котором находится запись|Теперь в цепочке присутствуют все три записи: договор, подпись пользователя, подтверждение владельца договора

#### Выход из договора, по инициативе пользователя

№|исполнитель|действие|результат|
-|-----------|--------|---------|
1|Пользователь|Создаёт запись, от имени нужного аккаунта, о желании выйти из договора
2|Майнер|Подписывает пакет, в котором находится запись|После подписания пакета, договор считается расторгнутым


#### Выход из договора, по инициативе владельца/администратора

№|исполнитель|действие|результат|
-|-----------|--------|---------|
1|Владелец/Администратор|Создаёт запись об исключении аккаунта из договора
2|Майнер|Подписывает пакет, в котором находится запись|После подписания пакета, договор считается расторгнутым, в отношении указанного аккаунта

#### Закрытие договора

№|исполнитель|действие|результат|
-|-----------|--------|---------|
1|Владелец/Администратор|Создаёт запись закрытии договора
2|Майнер|Подписывает пакет, в котором находится запись|После подписания пакета, договор считается закрытым

Договор может быть закрыт автоматически, без создания отдельных записей, если в нём указан период действия.

