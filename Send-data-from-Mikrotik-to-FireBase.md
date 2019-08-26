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
\"model\":\"$mkmdl\"}" url="https://YOUR-DATABASE.firebaseio.com/BRANCH-NAME/$mkserial.json"
```

Data on FireBase will look like this:

* BRANCH-NAME
   * 403107XXXXXX   **<-- Mikrotik Serial**
      * cvers: "6.44.5" 
      * date: "aug/26/2019" 
      * model: "RB750Gr3" 
      * name: "Public" 
      * time: "05:12:00" 
      * time: "05:12:00" 
      * verschan: "long-term" 

Basic security rules:

```
"BRANCH-NAME": {
   ".read": true,
      "$uid":{
      ".write": "$uid === $uid"
      }
```
