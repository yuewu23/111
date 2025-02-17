# Evaluation

We evaluate the effectiveness of the tool by answering the following questions:

- **RQ1:** How does the rendering performance of the layout improve after ffxing the hierarchical issues
using our method?

- **RQ2:** Does the layout maintain visual consistency with the original layout after the optimizing process?

For RQ1, we evaluate whether the rendering performance of the layout improves after ffxing the hierarchical issues using our method and whether LayoutOptimizer can effectively preserve the readability of UI code while optimizing Android layout issues.

For RQ2, we aim to evaluate whether the layout maintain visual consistency with the original layout after the optimizing process.

## Experimental Dataset Collection

App | Category                                                                                            | Layout                        
--- |-----------------------------------------------------------------------------------------------|--------------------------------------|
Simple Gallery Pro                          |Graphics           | activity_manage_folders, activity_widget_conffg
kotatsu                          |Reading            | activity_browser, activity_protect, activity_setup_protect
Stingle Photos                           |Multimedia                          |activity_backup_key, activity_camera_x, activity_gallery,activity_storage
Meshenger                           | Phone & SMS                          |activity_about, activity_backup, activity_call, activity_license,activity_main, activity_settings, activity_splash
home-assistant                           |Connectivity                           |activity_my, activity_settings, activity_webview
Catima                           |Money                          | about_activity, scan_activity, simple_toolbar_list_activity
Meditation Assistant                          | Time                           |activity_medinet, activity_progress, activity_complete
Gallery for PhotoPrism                          |Graphics                          | activity_destination_album_selection
Kitsune                           |Reading                           |activity_main
baresip+                          | Phone & SMS                          | activity_about
lespas                          | Multimedia                           |activity_main, activity_muzei_setting
Clock                          | Time                          | alarm_activity



In order to evaluate the effectiveness of this method, we selected 12 apps from the famous open source Android application website F-droid. The 12 apps belongs to seven categories: image, reading, multimedia, calling and texting, connectivity, and money management and time. The criteria for selecting these 12 apps from different domains were primarily based on their comparative standing with other apps within the same ffeld. A portion of these apps, such as Simple Gallery Pro, home-assistant, and kotatsu, boast download counts exceeding one million on Google Play Store. The other segment of apps, including Catima, MeditationAssistant, Meshenger, and StinglePhotos, have received a substantial number of positive reviews,with ratings above 4.5 on the Google Play Store.Additionally,all these apps are compatible with Android version 6.0 and above.From these apps,we manually screened the layouts according to the deffnitions of Redundant Containers (RCs) or Inappropriate Containers (ICs) within the layout graph. A total of 31 layouts containing RC or IC issues were selected for inclusion in the study. 

Our experimental machine is conffgured with 16GB memory, Intel Core i7-10700 64-bit CPU, and Windows 11. We set the population in the genetic algorithm to 100, iterate for a maximum of 1000 rounds, and terminate the search process with no better results for 200 consecutive rounds.


## RQ1: Rendering Performance and UI Code Readability Evaluation

To answer RQ1, we evaluate whether the rendering performance of the layout improves after fixing the hierarchical issues using our method and whether LayoutOptimizer can effectively preserve the readability of UI code while optimizing Android layout issues.To evaluate whether LayoutOptimizer can effectively preserve the readability of UI code while optimizing Android layout issues, we conducted an experiment in which developers rated the readability of the UI code.

### Rendering Performance

We implemented LayoutOptimizer as an Android library and compiled it into an Android Archive (AAR) file. Developers can conveniently optimize their layout performance by adding our AAR file as a dependency to their projects (as demonstrated in the open-source prototype of LayoutOptimizer). To utilize our tool, developers need to provide the Android runtime environment and relevant resources for the layout to be optimized. If you wish to use our tool, you can integrate our AAR file into your project as a dependency, copy our example code into a unit test, and modify the input to correspond with XML file from dataset.

We compare the rendering time spent in the layout-and-measure phase (abbreviated as rendering time) between origin layout and optimized layout on the Android emulator. The emulator we select is Pixel 2 (Android 11.0, 1.5GB RAM), which is a software-based tool that allows developers to simulate the behavior of a Google Pixel 2 device on their computer and is commonly used in Android app development to test applications. We use the high-resolution clock source System.nanoTime() provided by JAVA to accurately record the time spends in the layout-and-measure phase. For each layout, we render it 100 times, recording the time spent in the layout-and-measure phase for each rendering, and take the average as the ffnal result. In the experiment, the Androi API version is 30.0, the Java version is 1.8.

### UI Code Readability Evaluation

1.Participants recruitment: We posted a recruitment notice on Little Red Book , which included an introduction to LayoutOptimizer and a request for developers to rate some UI code. A total of 10 developers responded to the recruitment. After communication and assessment (such as their name, age, and development experience), we found that 4 of the developers had relatively limited experience. Therefore, we selected 6 developers with over 3 years of development experience, aged between 33 and 48, to participate in the experiment. Each participant will receive a $30 shopping card as a reward after completing the experiment.

2.Preparation: To ensure the smooth conduct of the experiment and protect the participants’ rights, we provided a brief training session before the experiment began. This training included an overview of the experiment and clear instructions on the task, informing participants that they would be asked to rate the readability of UI code on a scale from 1 to 5. We also assured participants that their personal information would only be used for this study and would not be used for any other purposes. Additionally, all participants in the user study signed an informed consent form. We provided detailed information about the study, including the research objectives, procedures, potential risks, and beneffts. Before voluntarily agreeing to participate, participants were allowed to ask questions and clarify any concerns. Furthermore, we ensured that participants’ identities were kept conffdential and would not be disclosed to anyone outside the research team. We also informed participants of their right to withdraw from the study at any time without any negative consequences.

3.Research settings: The study involved the following steps. First, we randomly selected one app from each of the seven categories in our dataset for evaluation. We then randomly divided the six participants into three groups, with two participants in each group, denoted as g1, g2, and g3. The apps required for the experiment were also divided into three groups (the ffrst two groups with two apps each, and the third group with three apps), labeled as a, b, and c, and further subdivided based on three types of UI code for each layout: a1, b1, c1 representing the original code, a2, b2, c2 representing the LayoutOptimizer-optimized code, and a3, b3, c3 representing the Baseline-optimized code. Participants in group g1 were responsible for rating a1, b2, and c3, group g2 rated a2, b3, and c1, and group g3 rated a3, b1, and c2. The assignment of apps to participants was completely randomized, and the evaluations were conducted in parallel. This grouping method aimed to effectively reduce participant bias due to memory, ensuring more controlled experimental results. Additionally, we assigned a staff member to each participant to assist with any issues that might arise during the rating process. The staff member’s role was to assist and clarify, without interfering with the participants’ evaluation process. After completing this process, we collected and analyzed the scores for all UI codes and visualized the results by creating box plots grouped by app categories.

### Baseline

In order to fully evaluate the optimization efect of our method on layout rendering, we introduced anothersimple layout optimization method as a baseline. This method uses ConstraintLayout to reconstruct thelayout into a single layer, removing all the remaining containers in the layout. The reason for adopting thismethod as a comparison approach is that reducing the hierarchy of layouts using ConstraintLayout is advo-cated by Google. The ConstraintLayout is the latest version androidx.constraintlayout:constraintlayout:2.0.4.

### Results
Layout | App | Original | Baseline | LayoutOpimizer                       
:---:|:---------------------:|:-----------------:|:----------------:|:--------------:|
activity_manage_folders<br>activity_widget_conffg   |Simple Gallery Pro  |501021<br>826072   | 675829<br>1378799   | 473415<br>743813
activity_backup_key<br>activity_camera_x<br>activity_gallery<br>activity_storage  |  Stingle Photos |  569605<br>321245<br>1326204<br>1038840 | 1300419<br> * <br>1158397<br>1117096 | 421982<br>122010<br>650983<br>744701
activity_browser<br>activity_browser<br>activity_setup_protect  |  Kotatsu |  609950 <br>1130539<br>1474307 |  * <br>1062295<br>1258988 | 271776<br>688052<br>845325
activity_about<br>activity_backup<br>activity_main<br>activity_call<br>activity_license<br>activity_settings<br>activity_splash  |  Meshenger |  995370 <br>2115979<br>909998<br>793538<br>817599<br>1557491<br>406002 |  1317053<br>1348845<br>844637<br>1091576<br>854752<br>3556986<br>749179 | 715396<br>1308954<br>232165<br>404606<br>382829<br>586056<br>293293
activity_my<br>activity_settings<br>activity_webview  |  home-assistant |  293787 <br>327974<br>228942 |  * <br>821959<br>603312 | 96255<br>219730<br>118923
activity_medinet<br>activity_progress<br>activity_complete  |  Meditation Assistant |  153501 <br>309203<br>1914306 |  318909 <br>488226<br>719963 | 96811<br>267092<br>655402
about_activity<br>scan_activity<br>simple_toolbar_list_activity  |  Catima |  941248 <br>268455<br>617956 |  1296352 <br>472351<br>850561 | 647161<br>142498<br>524787
activity_destination_album_selection   |  Gallery for PhotoPrism  |   463808  |   744560  |   432800
activity_main   |  Kitsune   |   985033  |   980103  |   561624
activity_about  |   baresip+   |   699768   |  916582   |  575495
activity_main<br>activity_muzei_setting   |lespas  |851249<br>742468   | 1358757<br>1344560   | 799835<br>45479
alarm_activity  |   Clock+   |   557834   |  956378   |  381858

It can be seen that all layouts optimized using our method achieved better rendering performance. The average rendering time of the original layout is 798364.258ns, while the average rendering time of the layout optimized by our method is 483111.065ns,
which reduces the rendering time by 39.49%. For the 31 layouts, our method resolved a total of 6 redundant container (RC) issues and 60 inappropriate container (IC) issues. It can be seen that the number of RC identiffed by our method is usually small. This is because our method follows a series of constraints during the identiffcation of RC, for example, a component with ID cannot be identiffed as RC. Although these constraints reduce the number of RC, they can avoid negative impact during the layout optimization.



## RQ2: Visual Consistency Maintaining Evaluation

Maintaining the visual consistency of the layout is an important goal of this paper when ffxing the hierarchical problem in the layout. In this RQ, we aim to evaluate whether the layout maintain visual consistency with the original layout after the optimizing process.


### Setup

Visual consistency maintaining consists of two progressive sub-goals, the ffrst sub-goal is to make the layout render the same for a speciffc screen size, and the second sub-goal is to make the layout render the same for all other screen sizes. The second sub-goal is important for layouts that are adaptable to different screen sizes. Android smartphones come in many different screen sizes, and it would be diﬀﬀcult to verify this 500 approach on all screen sizes. Therefore, we selected three screen sizes: 5.0 inches, 6.7 inches, and 6.4 inches, to verify the method’s ability to maintain layout visual consistency. According to the 2022 data, these three screen sizes are the most commonly used globally, accounting for 11.59%, 32.1%, and 16.1%, respectively. All layout optimization were performed on the Pixel 2 (5.0 inches). Therefore, to verify whether the method achieves the ffrst sub-goal, we evaluate whether the optimized layout has the same rendering effect as the original layout on the 5.0-inch screen. To verify the second sub-goal, we evaluate whether the optimized layout and the original layout have the same rendering effect on screens of 6.7 inches, 6.6 inches and 6.4 inches.

Our method only changes the size and position of components without modifying their visual attributes, such as background images, colors, or fonts. Therefore, to verify whether the rendering effects of the repaired layout and the original layout are the same, we only to compare the size and position of the components in the two layouts. Speciffcally, we measure the visual consistency of the repair layout based on the pixels occupied by each visual component (View or container with background, and its visibility attribute is True) before and after optimization. Speciffcally, if a pixel belongs to the same visual component in both the original and the optimized layout, we consider the pixel correct. 

### Results
Metric | Value                       
:---:|:---------------------:|
Precision (5.0 inch)  |  0.9766
Recall (5.0 inch)  |  0.9603
Precision (6.7 inch)  |  0.9580
Recall (6.7 inch)  |  0.9515
Precision (6.4 inch)  |  0.9617
Recall (6.4 inch)  |  0.9545

It can be seen that the average precision and recall of 5.0 inches are 0.9766 and 0.9603, respectively, indicating that the method can maintain visual consistency for a speciffc screen size. The average precision on 6.7-inch and 6.4-inch screens were 0.9580 and 0.9617, respectively; and the average recall on 6.7-inch and 6.4-inch screens were 0.9515 and 0.9545, respectively. This indicates that the method can also maintain visual consistency for different screen size.



