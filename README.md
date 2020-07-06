# Student Dropout Prediction

### Basic Information

Start: Jun 8, 2020 8:00 AM

End of preliminary contest: Oct 31, 2020 7:59 AM

Start of final contest: Nov 1, 2020 8:00 AM

End of final contest: Nov 2, 2020 8:00 AM

Date of final results: Nov 02, 2020 - Nov 15, 2020 

Rules: Only 3 submissions each day; Only 3 submissions in the final competition.

Acknowledgments: [XuetangX](https://next.xuetangx.com/) & [RCOE](http://www.rcoe.edu.cn/)

[Project URL](https://www.biendata.xyz/competition/chaindream_mooccube_task1/)

[Dataset Download](https://www.dropbox.com/s/5yz7c6aocplsqcj/Track1.zip?dl=0)

### Task

To predict if a student of XuetangX will dropout from a course based on their online learning behaviors in watching videos.

### Evaluation

Submissions are evaluated on one metric: acc(accuracy)

For a student i who takes 5 courses: course_i=(a,b,c,d,e)

Actual dropout situation is: dropout_i=(1,1,1,1,0)

Predicted dropout situation is: predict_i=(1,1,1,0,0)

acc_i=4/5=80%

For the whole dataset with n samples, acc = sum(acc_i)/n

**Submission file**

```json
{"label_list": [0, 1], "item_id": "T_53"}

# **"label_list": [1, 0, 1, 0]** : list type, the result of course dropout corresponding to each course in course_list.
# **"item_id": "T_53"** : corresponding to item_id in valid dataset
```

### Dataset

- Train dataset
    - **course_info.json**:

        course information dataset, each course has one json per line 

        1. **course_id**: string type，id of each course
        2. **item**: list type, each video and puzzle in the course, **V_**  starts with the video id, the order of this list represents the order in the actual course

        ```json
        {
        "course_id": "course-v1:JXUST+JXUST2016001+2016_T2",
        "item": ["V_a5c83a80e1734f3088a1e49f712439a6", "V_54610c0579ae49329e1938cbae56c929", "V_0f923cefe6dc44fdbd31f5d2db1c99b4", "V_5e18d5455bee435bb5f8a247c21bb984", ]
        }
        ```

    - **video_info.json**

        video information, each video has one json per line

        1. **id**: string type, the id of the video
        2. **name**: string type, the name of the video
        3. **text**: list type, each item is a string, the sentences of subtitles
        4. **start**: list type, each item is an int, the number of video frames at the beginning of each subtitle sentence
        5. **end**: list type, each item is an int, the number of video frames at the end of each subtitle sentence

        ```json
        {
        "id": "V_8a8d83a8e11146358238638e57d9996f",
        "name": "10xa1-5: 左倾性",
        "text": ["是的，借助NPL这个指标，我们就可以简明地定义什么叫做“左倾”，", "也就是说，对任何一个节点x，如果在NPL的意义上，它的左孩子不小于它的右孩子，", "我们就称之为“左倾”。", "如果在堆中，任何内部节点都是左倾的，", "我们就称这个堆为左倾堆，或者左式堆、左撇子堆，", "当然根据NPL的定义，既然每个节点的NPL值都是在它的孩子中间取一个小者，", "再累计上一个单位，于是很自然地在这个递推式中，", "我们只需考虑每个节点的右孩子，而忽略他的左孩子。", "不难确认，所谓的“左倾性”与我们此前的堆序性是彼此相容而不矛盾的。", "既然左倾性必须是处处满足的，因此我们自然可以推知，任何左式堆的任何一个子堆，", "必定依然是左式堆。", "不难理解，作为左式堆，它更倾向于将更多的节点分布于左侧的分支，", "正像我们最初所希望的那样。", "然而需要指出的是，这只是一个大致的倾向，事实情况未必严格如此，", "比如在课后你可以进一步来思考这样的两个问题：在左式堆中，是否左子堆的规模始终大于右子堆，", "另外左子堆的高度是否也必然总是大于右子堆？", "在这里，我们也给出了左式堆的具体实例，而刚才两个问题的答案也就藏在这个实例当中。"],
        "start": [4050, 13500, 26250, 29400, 35800, 43200, 55100, 62150, 68900, 79350, 90700, 95250, 106050, 109850, 120500, 134250, 143950],
        "end":[13500, 26250, 29400, 35800, 42550, 55100, 62150, 68900, 79350, 90700, 95250, 106050, 109850, 120500, 134250, 143950, 157550]
        }
        ```

    - **user_video_act_train_1.json** & **user_video_act_train_2.json**

        video watching activities for a student

        1. **activity**: list type, watching behaviors of all videos

            1.1 **course_id**: course id, the course one video belongs to

            1.2 **video_id**: video id, the id of each video

            1.3 **watching_count**: number of watching times for each video

            1.4 **video_duration**: the duration of this video

            1.5 **local_watching_time**: actual watching duration of each video (time spent on the video) 

            1.6 **video_progress_time**: actual watching duration of each video considering the playback speed

            1.7 **video_start_time**: the earliest time the user watched at each video

            1.8 **video_end_time**: the latest time the user watched at for each video

            1.9 **local_start_time**: actual watching start time 

            2.0 **local_end_time**: actual viewing end time

        2. **course_list**:list type, all courses the student watches
        3. **label_list**: list type, whether the user drops out after this video (predicted target)

        ```json
        {
        "activity": [
          {
            "course_id": "C_course-v1:TsinghuaX+30240184+sp",
            "video_id": "V_47135139ea7843ed9b38a8f48389abc7",
            "watching_count": 5,
            "video_duration": 163,
            "local_watching_time": 216,
            "video_progress_time": 212.4400007724762,
            "video_start_time": 0,
            "video_end_time": 163,
            "local_start_time": "2018-09-04 19:02:59",
            "local_end_time": "2018-09-04 19:12:18"
          },
          {
            "course_id": "C_course-v1:TsinghuaX+30240184+sp",
            "video_id": "V_4f184a3de72d418caccbd3fa8624d5b6",
            "watching_count": 2,
            "video_duration": 209,
            "local_watching_time": 65,
            "video_progress_time": 65.19000244140625,
            "video_start_time": 0,
            "video_end_time": 65.19000244140625,
            "local_start_time": "2018-09-04 18:59:23",
            "local_end_time": "2018-09-04 19:00:41"
          },
          {
            "course_id": "C_course-v1:TsinghuaX+30240184+sp",
            "video_id": "V_7321f00db10b461f93039df886fe9e8f",
            "watching_count": 1,
            "video_duration": 120,
            "local_watching_time": 120,
            "video_progress_time": 120,
            "video_start_time": 0,
            "video_end_time": 120,
            "local_start_time": "2018-09-04 19:00:48",
            "local_end_time": "2018-09-04 19:02:48"
          },
          {
            "course_id": "C_course-v1:TsinghuaX+30240184+sp",
            "video_id": "V_a7389b5205234b00873eadf9d0b0d802",
            "watching_count": 1,
            "video_duration": 281,
            "local_watching_time": 282,
            "video_progress_time": 281,
            "video_start_time": 0,
            "video_end_time": 281,
            "local_start_time": "2018-09-04 19:05:46",
            "local_end_time": "2018-09-04 19:10:28"
          }
        ],
        "course_list": [
          "C_course-v1:TsinghuaX+30240184+sp"
        ],
        "label_list": [
          0
        ]
        }
        ```

- Valid dataset
    - **user_video_act_val_triple_withId_noLabel_1**

        video watching activities for a student

        1. **activity**: list type, watching behaviors of all videos

            1.1 **course_id**: course id, the course one video belongs to

            1.2 **video_id**: video id, the id of each video

            1.3 **watching_count**: number of watching times for each video

            1.4 **video_duration**: the duration of this video

            1.5 **local_watching_time**: actual watching duration of each video (time spent on the video) 

            1.6 **video_progress_time**: actual watching duration of each video considering the playback speed

            1.7 **video_start_time**: the earliest time the user watched at each video

            1.8 **video_end_time**: the latest time the user watched at for each video

            1.9 **local_start_time**: actual watching start time 

            2.0 **local_end_time**: actual viewing end time

        2. **course_list**:list type, all courses the student watches
        3. **label_list**: list type, whether the user drops out after this video (predicted target)

        ```json
        {
          "course_list": [
            "C_course-v1:TsinghuaX+20430064X+sp",
            "C_course-v1:TsinghuaX+00680082X+sp"
          ],
          "activity": [
            {
              "video_start_time": 0,
              "local_start_time": "2016-04-16 15:20:03",
              "video_progress_time": 326,
              "local_watching_time": 328,
              "local_end_time": "2016-04-16 15:25:31",
              "course_id": "C_course-v1:TsinghuaX+20430064X+sp",
              "watching_count": 1,
              "video_end_time": 326,
              "video_id": "V_2b0abbba1fdb442cb483dd9129891827",
              "video_duration": 326
            },
            {
              "video_start_time": 0,
              "local_start_time": "2016-04-15 23:54:18",
              "video_progress_time": 196,
              "local_watching_time": 196,
              "local_end_time": "2016-04-15 23:57:34",
              "course_id": "C_course-v1:TsinghuaX+20430064X+sp",
              "watching_count": 1,
              "video_end_time": 196,
              "video_id": "V_2e55b72c02934e7bbfb4e8c964d92419",
              "video_duration": 196
            },
            {
              "video_start_time": 0,
              "local_start_time": "2016-04-11 01:39:54",
              "video_progress_time": 572,
              "local_watching_time": 573,
              "local_end_time": "2016-04-11 01:49:27",
              "course_id": "C_course-v1:TsinghuaX+00680082X+sp",
              "watching_count": 1,
              "video_end_time": 572,
              "video_id": "V_8271dd5223b84f91b991101f84b3b859",
              "video_duration": 572
            },
            {
              "video_start_time": 0,
              "local_start_time": "2016-04-11 01:49:37",
              "video_progress_time": 1209,
              "local_watching_time": 1209,
              "local_end_time": "2016-04-11 02:09:46",
              "course_id": "C_course-v1:TsinghuaX+00680082X+sp",
              "watching_count": 1,
              "video_end_time": 1209,
              "video_id": "V_a9ed6dd379674ef3a438801cec454502",
              "video_duration": 1209
            }
          ],
          "item_id": "T_53"
        }
        ```

