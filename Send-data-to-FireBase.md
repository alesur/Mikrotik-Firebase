# Send Data from Mikrotik to Firebase

```
:global mkserial [/system routerboard get serial-number]
:global mkname [/system identity get name]
:global mkupdiv [/system package update get installed-version]
:global mkupdch [/system package update get channel]
:global mkmdl [/system routerboard get mode]
:global timechk [/system clock get time]
:global datechk [/system clock get date]


/tool fetch http-method=put http-header-field="content-type:application/json" http-data="{
\"name\":\"$mkname\",
\"cvers\":\"$mkupdiv\",
\"verschan\":\"$mkupdch\",
\"time\":\"$timechk\",
\"date\":\"$datechk\",
\"model\":\"$mkmdl\"}" url="https://YOUR-DATABASE.firebaseio.com/BRANCH/$mkserial.json"
```

it will look like this

* BRANCH
   * 403107XXXXXX
      * Item 2b
