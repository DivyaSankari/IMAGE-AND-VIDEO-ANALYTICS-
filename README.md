# IMAGE-AND-VIDEO-ANALYTICS-
# Video Frame Information Extractor

This project involves a series of lab tasks aimed at extracting and analyzing video frame information using Python and ffmpeg. The tasks include setting up the environment, extracting frame information, analyzing frame types, visualizing frames, and studying frame compression.

## Lab Task 1: Setup and Basic Extraction

### Objective
Install the necessary tools and libraries, and extract frame information from a video.

### Steps
1. **Install ffmpeg and ffmpeg-python:**
   - Install the ffmpeg tool and the ffmpeg-python library.
     ```sh
     sudo apt-get install ffmpeg
     pip install ffmpeg-python
     ```

2. Extract Frame Information:
   - Use the provided script to extract frame information from a sample video.
     ```python
     import subprocess
     import json

     def extract_frames_info(video_path):
         try:
             result = subprocess.run(
                 ['ffprobe', '-v', 'error', '-select_streams', 'v:0', '-show_entries', 'stream=width,height,r_frame_rate,nb_frames', '-of', 'json', video_path],
                 stdout=subprocess.PIPE,
                 stderr=subprocess.PIPE,
                 check=True
             )

             probe = json.loads(result.stdout)
             video_stream = probe['streams'][0]
             width = video_stream['width']
             height = video_stream['height']
             r_frame_rate = video_stream['r_frame_rate']
             nb_frames = int(video_stream['nb_frames'])

             num, denom = map(int, r_frame_rate.split('/'))
             frame_rate = num / denom

             return {
                 'width': width,
                 'height': height,
                 'frame_rate': frame_rate,
                 'nb_frames': nb_frames
             }

         except subprocess.CalledProcessError as e:
             print(f"Error occurred: {e.stderr.decode()}")
             return None

     video_info = extract_frames_info('your_video_file.mp4')
     if video_info:
         print(video_info)
     ```

## Lab Task 2: Frame Type Analysis

### Objective
Analyze the extracted frame information to understand the distribution of I, P, and B frames in a video.

### Steps
1. Modify the Script:
   - Count the number of I, P, and B frames.
   - Calculate the percentage of each frame type in the video.

2. Analyze Frame Distribution:
   - Plot the distribution of frame types using a library like matplotlib.
   - Plot a pie chart or bar graph showing the distribution of frame types using matplotlib.

## Lab Task 3: Visualizing Frames

### Objective
Extract actual frames from the video and display them using Python.

### Steps
1. Extract Frames:
   - Use ffmpeg to extract individual I, P, and B frames from the video.
   - Save these frames as image files.

2. Display Frames:
   - Use a library like PIL (Pillow) or opencv-python to display the extracted frames.

### Tasks
1. Save I, P, and B frames as separate image files using ffmpeg.
2. Use PIL or opencv-python to load and display these frames in a Python script.
3. Compare the visual quality of I, P, and B frames.

## Lab Task 4: Frame Compression Analysis

### Objective
Analyze the compression efficiency of I, P, and B frames.

### Steps
1. Calculate Frame Sizes:
   - Calculate the file sizes of extracted I, P, and B frames.
   - Compare the average file sizes of each frame type.

2. Compression Efficiency:
   - Discuss the role of each frame type in video compression.
   - Analyze why P and B frames are generally smaller than I frames.

## Lab Task 5: Advanced Frame Extraction

### Objective
Extract frames from a video and reconstruct a part of the video using only I frames.

### Steps
1. Extract and Save I Frames:
   - Extract I frames from the video and save them as separate image files.

2. Reconstruct Video:
   - Use the extracted I frames to reconstruct a portion of the video.
   - Create a new video using these I frames with a reduced frame rate.

---

By completing these tasks, you will gain a comprehensive understanding of video frame extraction, analysis, and visualization using Python and ffmpeg.

