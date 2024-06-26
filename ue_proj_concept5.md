# Вторая часть концепта(переделанная (ещё раз(ещё раз)))
![abstruct_entities](./docs/abstruct_entities4.png)

## BaseCharacter
(Класс описыващий характер всех существ в данной игре)

### Поля
- BaseStatsComponent
- WeaponManagerComponent

## BaseStatsComponent
(Компонента, которая в себе объединяет две базовые компаненты это здоровье и устойчивость)

### Поля
- HPManagerComponent
- ResistenceManagerComponent

## ResistanceManagerComponent
(Компонета, описывающая хранение и работу с устойчивостью для существ)

### Поля
- Resistance - это константа с которой есть устойчивость к урону, если она равна 0, то сущность получает полный урон, если 1 то получает damage-1 и тд.

### Методы
- setResistance(float) - поставить новый уровень устойчивости

## HPManagerComponent
(Компонета, описывающая хранение и работу со здоровьем для существ)

### Поля
- HP - уровень здоровья, не восставнавливается сомостоятельно, если конечно не обговорены частные случаи
- MaxHP - верхняя грань по количесву здоровья

### Методы
- addHP(float delta) - если дельта положительна то персонаж хилится, инaче теряет едииницы по соответсвующей шкале

## WeaponManagerComponent
(Сущность для объединении и работы с оружиями)

### Поля
- Weapons - список всех оружий в данной момент у существа

### Поля
- ChangeWeapon - поменять оружие которое стоит на руках 
- Attack - функция для совершения выстрела с помощью оружия

## WeaponComponent
(Компонента отвечающая за оружия и взаимодействия с ними)

### Поля
- Skeletal Mesh - это структура скелета оружия 
- AmountOfEnergy - какая-то определённая константа, которая будет говорить сколько энергии надо отнять от владельца оружия энергии для совершения выстрела
- HitPerTick - это частота удара или выстрала с помощью оружия

### Методы
- ToHit() - совершить выстрел, будет смотреть если величина (AmountOfEnergy * IsPlayer()(вернёт true если носитель это главный герой)) <= Enengy(поле у носителя), то совершит выстрел  

## MeleeWeaponComponent
(От этого компонета будут наследоваться все остальные оружия ближнего боя)
(сделать так, чтобы при ударе опонента и при этом носитель оружия находится в движении и перед ударом он отпустил кнопку движения то он наносить урон с учётом скорости с которой он двигался к врагу, а-ля передаётся импульс движения в удар)

### Поля
- Damage - урон наносимый за один удар

## GunWeaponComponent
(От этого компонета будут наследоваться все остальные оружия дистанционного боя)

### Поля
- SpeedOFBullet - скорость полёта пули

## Player
(Это сущность отвесающая за главного персонажа, наследник класса BaseCharacter)

### Поля
- EnergyManagerComponent
- ShieldManagerComponent
- AbitilyMAnagerComponent

## EnergyManagerComponent
(Компонета, описывающая хранение и работу с энергией для персонажа)

### Поля
- Energy - уровень энергии, необходимо для совершения выстрела, не восстанавливается сомостоятельно, если конечно не обговорены частные случаи. В случае главного героя, после убийства врагов есть шанс увеличения энергии.
- MaxEnergy - верхняя грань по количесву энергии

### Методы
- addEnergy(float delta) - если дельта положительна то у персонажа увеличивается количесво энергии, инaче теряет едииницы по соответсвующей шкале

## ShieldManagerComponent
(Комаонента, описывающая хранение и работу с бронёй для персонажа)

### Поля
- Shield - уровень щита, при получении урона в начале теряет единицы щит и если щит уже пал, то теряется здоровье. Если персонаж не получает урона, то его щит начаинает восстанавливаться.
- MaxShield - верхняя грань по количесву брони

### Методы
- addShield(float delta) - если дельта положительна то у персонажа увеличивается количесво щита, инaче теряет едииницы по соответсвующей шкале

## AbilityManagerComponent
(Сущность отвечающая за способности персонажа и взаимодействие с ними)

### Поля
- Abilities - множество компонет способностей персонажа

### Методы
- UseAbility() - функция которая вызовет аналогичный метод у конкретной способности

## AbilityComponent
(Это сущность отвечающая за способность с которой зашёл на прохождение главный герой. От этой сущности будут наследоваться все остальные способности. У данной сущности нет полей так как каждая способность может иметь свои уникальные фишки и общих черт между всеми может и не быть.)

### Методы
- UseAbility() - виртуальная функция для активации способности

## Enemy
(Это сущность отвечающая за абстрактное представление всех врагов. От этой сущности будут наследоваться все остальные враги.)

### Поля
- AIController - сущность отвечающая за поведение конкретного врага

## GameManager
("Режиссер игры", т.е. это та сущность, которая будет упровлять всей игрой и развлекать главного героя)

### Поля
- BonusManagerComponent
- RoomManagerComponent

## BonusManagerComponent
(Сущность, которая объединяет в себе все бонусы полученные главным героем за время прохождения комнат и взаимодействие с ними)

### Поля
- Bonuses - множество бонусов у персонажа

### Методы
- ActivateBonus - функция которая вызовет аналогичный метод у конкретного бонуса

## BonusComponent
(Это сущность отвечающая за бонусы которые будет получать главный герой по мере прохождения комнат. От этой сущности будут наследоваться все остальные бонусы. У данной сущности нет полей так как каждый бонус может иметь свои уникальные фишки и общих черт между всеми может и не быть. Возможно получение каких-то определённых бонусов можно будеть получать ачивочки, и если получить все виды бонусов можно будет получить отдельную ачивочку, но это на будущее идея.)

### Методы
- ActivateBonus() - виртуальная функция для использования бонуса 

## RoomsManager
(Сущность, которая объединяет в себе все комнаты и взаимодействие с ними)

### Поля
- Rooms - комнаты, которые были пораждены по мере прохождений их главным героем

### Методы 
- createNextRoom() - создание следующей комнаты

## Room
(Это сущность отвечающая за абстрактное представление всех комнат. От этой сущности будут наследоваться все остальные комнаты. Все остальные уникальные фишки будут определяться отдельно для каждой комнаты.)

### Поля
- RoomManager
- InDoor - это координаты места входа в комнаты (мб не нужна будет тк главный герой всё равно не может возвращаться назад)
- OutDoor - это дверь выхода, для начала сделаю просто как отметину на полу для, после дороботаю

### Методы
- LetLeave - функция, чтобы выпустить главного героя из комнаты, только если главный герой выполнил все необходимые условия для этого
- LetGoInto - функция, чтобы впустить главного героя в комнату

## RoomManager
(Сущность, которая объединяет в себе управление всеми врагами и платформами в данной комнате)

### Поля
- PlatformManager
- EnemyManagerController

## PlatformManager
(Сущность, для хранении и управлении всеми клатформами в данной команате)

### Поля
- Platforms - платформы, которые есть в данной комнате

### Методы
- ActivateAllPlatforms() - вызовится данный метод, когда главный герой будет совершать вход в комнату, и этот метод просто спавнит все платформы и активирует их всех(ну те платформы, которые должны двигаться, начнут двигаться)

## Platform
(Сущность для предстваления платвормы. Нельзя будет ставить экземпляр этого класса тк, сама по себе она ничего не представляет.)

### Поля
- hasCollision - логическая переменная отвечающая за присутствие колизии у текущей платформы

## EnemyManagerController
(Сущность для работы со всеми врагами в комнате)

### Поля
- EnemyManagers - все менеждеры врагов

## EnemyManager
(Сущность, которая контролирует поведение конкретного врага)

### Поля
- CurrentEnemy - Сам враг собственной персоной
- EnemyController

### Методы
- `spawn<TEnemy>(FVector loc)` - создание врага в определённой локации

## EnemyController
(Отвечает за поведение врага и его логику)
// не знаю что надо тут описать