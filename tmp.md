# Bit of docs.
## Custom objects
### Workplace *[Workplace__c]*

> Используется для второй авторизации пользователей.

#### Поля:
- *Login__c* [Text(64) (Unique Case Insensitive)]
- *Operator__c* [Lookup(Contact)]
- *Password__c* [Text (Encrypted)(175)]
- *PhoneLine__c* [Text(250)]
- *Type__c* [Picklist : {Operator(Default), Manager, Other}]

> В очереди используются только экземпляры `Workplace__c` со значением `Operator` поля `Type__c`

### Session *[Session__c]*

> Используется для учета активных пользователей в текущий момент для второй авторизации.

#### Поля:
- *Status__c* [Picklist : {Active(Default), Closed, Ready, Paused, Busy}]
- *User_SF__c* [Lookup(User)]
- *User_Name__c* [Text(255)]
- *Workplace__c* [Lookup(Workplace)]

### Activity *[Activity__c]*

> Используется для связи конкретного оператора с конкретной задачей.

#### Поля:
- *StartDate__c* [Date/Time]
- *EndDate__c* [Date/Time]
- *RecordedCall__c* [URL(255)]
- *Status__c* [Picklist : {New(Default), Active, Closed}]
- *Type__c* [Text(100)]
- *Workplace__c* [Lookup(Workplace)]

### Message *[Message__c]*

> Используется как универсальный объект для хранения сообщений с различных источников. Источники разграничиваются с помощью RecordType-ов.

#### Поля:
- *CheckTime__c* [Text(250)]
- *Contact__c* [Lookup(Contact)]
- *Cost__c* [Number(16, 2)]
- *crc__c* [Text(100) (External ID)]
- *FacebookThread__c* [Text(250)]
- *Key__c* [Text(250)]
- *MessageText__c* [Long Text Area(32000)]
- *Operator__c* [Text(250)]
- *PhoneNumber__c* [Text(250)]
- *Received__c* [Text(250)]
- *SendDate__c* [Text(250)]
- *Sender__c* [Text(250)]
- *Sent__c* [Text(250)]
- *SiteName__c* [Text(250)]
- *Status__c* [Picklist : {New(Default), Responded, Read, Invalid}]
- *Time__c* [Date/Time]
- *VirtualNumber__c* [Text(250)]

#### Record Types:
- *Incoming SMS Message* [Record type for incoming SMS]
- *Outcoming SMS Message* [Record type for outcoming SMS]
- *Regular Message* [Just regular message with all fields.]
- *Skype* [Record type for Skype messages.]

## Custom settings
### Redirect Settings *[RedirectSettings__c]*

>Используются для редиректов при нажатии кнопки `Начать` на странице оператора.

#### Поля:
- *Key__c* [Text(250)]
- *Target__c* [URL(255)]

В качестве ключа для поиска используется первая часть поля `Type__c` объекта `Activity__c` : `<Тип источника>:<Идентификатор>`
Например: 
- Skype : `Skype:heykak`
- SMS : `SMS:380967775566`

Обязательный екземпляр - _**Default**_

``` 
Key = "Default"
Target = "https://cs17.salesforce.com/003/e"
```

### Key-Value Settings *[KVSettings__c]*

>Используются как хранилище типа ключ-значение для более гибкой настройки(без изменение кода классов и триггеров).

#### Поля:
- *Key__c* [Text(250)]
- *Value__c* [Text(250)]

__Необходимые екземпляры:__

*Default Activity__c Owner*
```
Key = "OwnerID" //
Value = "00520000003HCWX" //ID of SF User
```

*Incoming SMS Message*
```
Key = "inSMSMessage" //
Value = "012g0000000CzIAAA0" //Message__c RecordTypeID for Incoming SMS message
```

*Outcoming SMS Message*
```
Key = "outSMSMessage" //
Value = "012g0000000CzKpAAK" //Message__c RecordTypeID for Outcoming SMS message
```

*Regular Message*
```
Key = "RegularMessage" //
Value = "012g0000000CzI5AAK" //Message__c RecordTypeID for Regular message
```

*Skype message*
```
Key = "Skype" //
Value = "012g0000000Czf4AAC" //Message__c RecordTypeID for Skype message
```

*Skype message owner*
```
Key = "demitros07" //Skype login
Value = "00520000003HCWX" //ID of SF User
```

*Message Queue*
```
Key = "MessageQueue" //
Value = "00Gg0000000eFPxEAM" //Queue ID
```
