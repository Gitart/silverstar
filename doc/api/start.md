## POST box


```
curl  -X POST \
      -d "{name:NewlyNamedBox, notes:AdditionalNotesText, stageKey:5002}"  \
      -u YOUR_API_KEY: \
      -H "Content-Type:application/json" \
      https://www.streak.com/api/v1/boxes/{boxKey}
```      

## Request sample

```
{
  "pipelineKey": "agptYWlsZm9vZ2FlcioLEgxPcmdhbml6YXRpb24iCnN0cmVhay5jb20MCxIIV29ya2Zsb3cYPww",
  "creatorKey": "agptYWlsZm9vZ2FlciYLEgxPcmdhbml6YXRpb24iCnN0cmVhay5jb20MCxIEVXNlchgBDA",
  "creationTimestamp": 1348436318347,
  "lastUpdatedTimestamp": 1348441203844,
  "name": "NewlyNamedBox",
  "notes": "AdditionalNotesText",
  "stageKey": "5002",
  "fields": {},
  "followerKeys": [],
  "followerCount": 0,
  "commentCount": 0,
  "taskTotal": 0,
  "gmailThreadCount": 1,
  "fileCount": 0,
  "boxKey": "agptYWlsZm9vZ2FlcicLEgxPcmdhbml6YXRpb24iCnN0cmVhay5jb20MCxIEQ2FzZRiZAQw",
  "key": "agptYWlsZm9vZ2FlcicLEgxPcmdhbml6YXRpb24iCnN0cmVhay5jb20MCxIEQ2FzZRiZAQw"
}
```
