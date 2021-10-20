Deep Emoji
---------------
DeepMoji is a model trained on 1.2 billion tweets with emojis to understand how language is used to express emotions. Through transfer learning the model can obtain state-of-the-art performance on many emotion-related text modeling tasks.<br>
This application is developed based on open source project [DeepMoji](https://github.com/bfelbo/DeepMoji)<br>
REST APIs are additionally developed as part of this application for consumption by other producer applications running in MEC edge platform.<br>

Usage Steps:
--------------
<h4> Get emoji based on input sentence</h4>
Step 1: Provide input (as senetnce in text format) for getting emoji prediction and obtain top 5 emoji class and it's confidence interval (URI: /deepmoji/v1/input) <br>
Step 2: Provide input class (as number) for image of emoji and get output image of an emoji (URI: /deepmoji/v1/getmoji) <br>

Deep Emoji Interface 
----------------
<h4>1. Get emoji classes (identifier of emoji images) for given sentence</h4>
Input the text and obtain the top 5 emoji prediction class <br>

Resource URI: /deepmoji/v1/input<br>
Method: POST<br>

Body Parameters:

| Name          | Type                        | Description              | Required      |
| ------------- | --------------------------- | ------------------------ | ------------- |
| text    | text  | text   | Yes |

Return Parameters:

| Name          | Type                        | Description              |
| ------------- | --------------------------- | ------------------------ |
| Emoji     | object    | top 5 emoji class  |
| class | int | class that sentence belongs to  |
| Confidence Interval | float | confidence interval of the class  |

Example Request:

```
curl -X 'POST'
  'http://{{HOST_IP}}:{{PORT}}/faceDetection/v1/video/input'
  -H 'accept: application/json'
  -H 'Content-Type: application/x-www-form-urlencoded'
  -d 'text=This%20is%20the%20shit!'
```

Example Response:

```
HTTP/1.1 200 OK
{
    "Emoji_1": {
        "class": 51,
        "confidenceInterval": 9.83514
    },
    "Emoji_2": {
        "class": 0,
        "confidenceInterval": 7.05356
    },
    "Emoji_3": {
        "class": 3,
        "confidenceInterval": 5.01196
    },
    "Emoji_4": {
        "class": 38,
        "confidenceInterval": 4.89525
    },
    "Emoji_5": {
        "class": 44,
        "confidenceInterval": 3.4059
    }
}
```

<h4>2. Get emoji image</h4>
Input the emoji class and obtain coressponding emoji class's image<br>

Resource URI: /deepmoji/v1/getmoji<br>
Method: POST<br>

Body Parameter:

| Name          | Type                        | Description              | Required      |
| ------------- | --------------------------- | ------------------------ | ------------- |
| class    | text                      | the value should be in the range of classification (0-63) to get the image of an emoji   | Yes |

Return Parameters:

| Name          | Type                        | Description              |
| ------------- | --------------------------- | ------------------------ |
| file     | file                     | output file                |

Example Request:

```
curl -X 'POST'
  'http://{{HOST_IP}}:{{PORT}}/deepmoji/v1/getmoji'
  -H 'accept: application/json'
  -H 'Content-Type: application/x-www-form-urlencoded'
  -d 'class=27'
```

Example Response:

```
HTTP/1.1 200 OK
<<File output>>
```
