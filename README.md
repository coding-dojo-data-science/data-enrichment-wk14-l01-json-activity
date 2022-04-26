# JSON & APIs Activity - Solution

<img src="Images/youll-be-back-plus-cast.jpg"  width=70%> 
<center><a href="http://images.genius.com/bfcf74e4a3ff5662ca4a31700590a1de.1000x330x1.jpg">Image Source</a></center>

## JSON

### Reading JSON files

Import JSON library. Also, import Pandas.


Load JSON from file ('spotify_song_analysis.json'). This file contains song data from Spotify on You'll Be Back from the musical Hamilton.


```python
import json
import pandas as pd


json_file='Data/spotify_song_analysis.json'

with open(json_file,'r') as file:
    json_file = file.read()
    data = json.loads(json_file)
```

Print out data.


```python
print(data)
```

    {'meta': {'analyzer_version': '4.0.0', 'platform': 'Linux', 'detailed_status': 'OK', 
    ...
     {'start': 204.93008, 'duration': 0.32832, 'confidence': 0.337}, {'start': 205.2584, 'duration': 0.16416, 'confidence': 0.337}, {'start': 205.42258, 'duration': 0.32832, 'confidence': 0.372}, {'start': 205.7509, 'duration': 0.32832, 'confidence': 0.372}]}


Check type of data, get keys.


```python
type(data)
```




    dict




```python
data.keys()
```




    dict_keys(['meta', 'track', 'bars', 'beats', 'sections', 'segments', 'tatums'])



Explore 'meta' by printing it out, checking its type and keys.


```python
type(data['meta'])
```




    dict




```python
data['meta'].keys()
```




    dict_keys(['analyzer_version', 'platform', 'detailed_status', 'status_code', 'timestamp', 'analysis_time', 'input_process'])



Now use the 'track' key to inspect details about the song.
- What key is the song in?


```python
data['track'].keys()
```




    dict_keys(['num_samples', 'duration', 'sample_md5', 'offset_seconds', 'window_seconds', 'analysis_sample_rate', 'analysis_channels', 'end_of_fade_in', 'start_of_fade_out', 'loudness', 'tempo', 'tempo_confidence', 'time_signature', 'time_signature_confidence', 'key', 'key_confidence', 'mode', 'mode_confidence', 'codestring', 'code_version', 'echoprintstring', 'echoprint_version', 'synchstring', 'synch_version', 'rhythmstring', 'rhythm_version'])



| ID | Key   |
|------|------|
| 0 | C |
1 |	C♯ 
2  | D 
3  | D♯
4  | E 
5  | F 
6  | F♯
7  | G
8  | G♯
9  | A
10 | A♯	
11 | B 	


```python
data['track']['key']
```




    0



How long is the song?


```python
data['track']['duration']
```




    208.32109



Load the 'track' data into a DataFrame.


```python
df = pd.DataFrame.from_dict(data['track'], orient='index')
df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>num_samples</th>
      <td>4593480</td>
    </tr>
    <tr>
      <th>duration</th>
      <td>208.32109</td>
    </tr>
    <tr>
      <th>sample_md5</th>
      <td></td>
    </tr>
    <tr>
      <th>offset_seconds</th>
      <td>0</td>
    </tr>
    <tr>
      <th>window_seconds</th>
      <td>0</td>
    </tr>
    <tr>
      <th>analysis_sample_rate</th>
      <td>22050</td>
    </tr>
    <tr>
      <th>analysis_channels</th>
      <td>1</td>
    </tr>
    <tr>
      <th>end_of_fade_in</th>
      <td>0.12186</td>
    </tr>
    <tr>
      <th>start_of_fade_out</th>
      <td>204.89288</td>
    </tr>
    <tr>
      <th>loudness</th>
      <td>-7.562</td>
    </tr>
    <tr>
      <th>tempo</th>
      <td>121.741</td>
    </tr>
    <tr>
      <th>tempo_confidence</th>
      <td>0.234</td>
    </tr>
    <tr>
      <th>time_signature</th>
      <td>4</td>
    </tr>
    <tr>
      <th>time_signature_confidence</th>
      <td>0.981</td>
    </tr>
    <tr>
      <th>key</th>
      <td>0</td>
    </tr>
    <tr>
      <th>key_confidence</th>
      <td>0.381</td>
    </tr>
    <tr>
      <th>mode</th>
      <td>1</td>
    </tr>
    <tr>
      <th>mode_confidence</th>
      <td>0.636</td>
    </tr>
    <tr>
      <th>codestring</th>
      <td>eJw1mgmS7SgMBK_iI7Av979YZxavJ2J-NDwbg5ZSSaKWvV...</td>
    </tr>
    <tr>
      <th>code_version</th>
      <td>3.15</td>
    </tr>
    <tr>
      <th>echoprintstring</th>
      <td>eJzNvQuu7TqOZdsl2_pYao5-7n8T3hg-iYfKLFgLqI1AVV...</td>
    </tr>
    <tr>
      <th>echoprint_version</th>
      <td>4.12</td>
    </tr>
    <tr>
      <th>synchstring</th>
      <td>eJxlWYmN4zAMbMUlWKLe_hs7zsMkiwOyC0fWw3c4VHp_5_...</td>
    </tr>
    <tr>
      <th>synch_version</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>rhythmstring</th>
      <td>eJxVmwmSWzkMQ6_iI2hf7n-xIfCo35mqpJJ22_oSRYIgSN...</td>
    </tr>
    <tr>
      <th>rhythm_version</th>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
pd.DataFrame(data['track'],index=[0]).T
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>num_samples</th>
      <td>4593480</td>
    </tr>
    <tr>
      <th>duration</th>
      <td>208.32109</td>
    </tr>
    <tr>
      <th>sample_md5</th>
      <td></td>
    </tr>
    <tr>
      <th>offset_seconds</th>
      <td>0</td>
    </tr>
    <tr>
      <th>window_seconds</th>
      <td>0</td>
    </tr>
    <tr>
      <th>analysis_sample_rate</th>
      <td>22050</td>
    </tr>
    <tr>
      <th>analysis_channels</th>
      <td>1</td>
    </tr>
    <tr>
      <th>end_of_fade_in</th>
      <td>0.12186</td>
    </tr>
    <tr>
      <th>start_of_fade_out</th>
      <td>204.89288</td>
    </tr>
    <tr>
      <th>loudness</th>
      <td>-7.562</td>
    </tr>
    <tr>
      <th>tempo</th>
      <td>121.741</td>
    </tr>
    <tr>
      <th>tempo_confidence</th>
      <td>0.234</td>
    </tr>
    <tr>
      <th>time_signature</th>
      <td>4</td>
    </tr>
    <tr>
      <th>time_signature_confidence</th>
      <td>0.981</td>
    </tr>
    <tr>
      <th>key</th>
      <td>0</td>
    </tr>
    <tr>
      <th>key_confidence</th>
      <td>0.381</td>
    </tr>
    <tr>
      <th>mode</th>
      <td>1</td>
    </tr>
    <tr>
      <th>mode_confidence</th>
      <td>0.636</td>
    </tr>
    <tr>
      <th>codestring</th>
      <td>eJw1mgmS7SgMBK_iI7Av979YZxavJ2J-NDwbg5ZSSaKWvV...</td>
    </tr>
    <tr>
      <th>code_version</th>
      <td>3.15</td>
    </tr>
    <tr>
      <th>echoprintstring</th>
      <td>eJzNvQuu7TqOZdsl2_pYao5-7n8T3hg-iYfKLFgLqI1AVV...</td>
    </tr>
    <tr>
      <th>echoprint_version</th>
      <td>4.12</td>
    </tr>
    <tr>
      <th>synchstring</th>
      <td>eJxlWYmN4zAMbMUlWKLe_hs7zsMkiwOyC0fWw3c4VHp_5_...</td>
    </tr>
    <tr>
      <th>synch_version</th>
      <td>1.0</td>
    </tr>
    <tr>
      <th>rhythmstring</th>
      <td>eJxVmwmSWzkMQ6_iI2hf7n-xIfCo35mqpJJ22_oSRYIgSN...</td>
    </tr>
    <tr>
      <th>rhythm_version</th>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



### Using the 'spotify_song_analysis.json' file and what you have learned above, do the following:

#### Create a DataFrame of the different segments of the song


```python
data.keys()
```




    dict_keys(['meta', 'track', 'bars', 'beats', 'sections', 'segments', 'tatums'])




```python
df = pd.DataFrame.from_records(data['segments'])
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>start</th>
      <th>duration</th>
      <th>confidence</th>
      <th>loudness_start</th>
      <th>loudness_max_time</th>
      <th>loudness_max</th>
      <th>loudness_end</th>
      <th>pitches</th>
      <th>timbre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.00000</td>
      <td>0.12186</td>
      <td>0.000</td>
      <td>-60.000</td>
      <td>0.00000</td>
      <td>-60.000</td>
      <td>0.0</td>
      <td>[0.794, 0.306, 0.104, 0.068, 0.042, 0.102, 0.2...</td>
      <td>[0.069, 170.355, 10.68, -30.205, 57.752, -50.9...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.12186</td>
      <td>0.89950</td>
      <td>1.000</td>
      <td>-60.000</td>
      <td>0.03009</td>
      <td>-14.000</td>
      <td>0.0</td>
      <td>[0.017, 0.014, 1.0, 0.049, 0.028, 0.054, 0.077...</td>
      <td>[37.897, 4.049, 12.196, 112.018, 49.354, 20.24...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1.02136</td>
      <td>1.13188</td>
      <td>0.098</td>
      <td>-34.547</td>
      <td>0.04109</td>
      <td>-32.755</td>
      <td>0.0</td>
      <td>[0.018, 0.022, 0.734, 0.041, 0.04, 0.084, 0.08...</td>
      <td>[23.706, -43.506, 51.752, 63.628, 54.967, -31....</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2.15324</td>
      <td>0.54703</td>
      <td>1.000</td>
      <td>-43.067</td>
      <td>0.04015</td>
      <td>-15.593</td>
      <td>0.0</td>
      <td>[0.032, 0.008, 0.324, 0.035, 0.025, 1.0, 0.034...</td>
      <td>[39.471, -30.634, 10.759, 43.412, 26.225, 9.94...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2.70027</td>
      <td>1.47968</td>
      <td>0.075</td>
      <td>-29.893</td>
      <td>0.05629</td>
      <td>-27.711</td>
      <td>0.0</td>
      <td>[0.111, 0.029, 0.857, 0.051, 0.064, 1.0, 0.061...</td>
      <td>[27.067, -33.494, -21.14, 72.879, 27.074, -36....</td>
    </tr>
  </tbody>
</table>
</div>



#### Find the longest segment and the loudest segment.


```python
df.sort_values('loudness_max',ascending=False).head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>start</th>
      <th>duration</th>
      <th>confidence</th>
      <th>loudness_start</th>
      <th>loudness_max_time</th>
      <th>loudness_max</th>
      <th>loudness_end</th>
      <th>pitches</th>
      <th>timbre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>653</th>
      <td>187.24059</td>
      <td>0.31238</td>
      <td>0.599</td>
      <td>-5.943</td>
      <td>0.03607</td>
      <td>0.267</td>
      <td>0.0</td>
      <td>[0.461, 0.144, 0.085, 0.243, 1.0, 0.289, 0.156...</td>
      <td>[57.602, 55.587, 85.821, 22.038, 33.303, -26.8...</td>
    </tr>
    <tr>
      <th>649</th>
      <td>186.29356</td>
      <td>0.40063</td>
      <td>0.233</td>
      <td>-4.058</td>
      <td>0.03451</td>
      <td>0.097</td>
      <td>0.0</td>
      <td>[0.22, 0.074, 0.327, 0.072, 0.111, 1.0, 0.28, ...</td>
      <td>[57.562, 60.103, 65.943, 27.043, 23.254, -38.0...</td>
    </tr>
    <tr>
      <th>661</th>
      <td>190.21365</td>
      <td>0.30005</td>
      <td>0.399</td>
      <td>-5.091</td>
      <td>0.10304</td>
      <td>-0.049</td>
      <td>0.0</td>
      <td>[0.091, 0.266, 0.349, 0.442, 0.476, 0.39, 1.0,...</td>
      <td>[58.074, 40.614, 59.928, 2.244, 34.151, -41.53...</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.nlargest(1,['loudness_max'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>start</th>
      <th>duration</th>
      <th>confidence</th>
      <th>loudness_start</th>
      <th>loudness_max_time</th>
      <th>loudness_max</th>
      <th>loudness_end</th>
      <th>pitches</th>
      <th>timbre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>653</th>
      <td>187.24059</td>
      <td>0.31238</td>
      <td>0.599</td>
      <td>-5.943</td>
      <td>0.03607</td>
      <td>0.267</td>
      <td>0.0</td>
      <td>[0.461, 0.144, 0.085, 0.243, 1.0, 0.289, 0.156...</td>
      <td>[57.602, 55.587, 85.821, 22.038, 33.303, -26.8...</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.sort_values('duration',0,0).head(3)
```

    /var/folders/rf/vw4r41jd7vd95x1w0dth7v9h0000gp/T/ipykernel_17270/2160200358.py:1: FutureWarning: In a future version of pandas all arguments of DataFrame.sort_values except for the argument 'by' will be keyword-only
      df.sort_values('duration',0,0).head(3)





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>start</th>
      <th>duration</th>
      <th>confidence</th>
      <th>loudness_start</th>
      <th>loudness_max_time</th>
      <th>loudness_max</th>
      <th>loudness_end</th>
      <th>pitches</th>
      <th>timbre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>699</th>
      <td>205.36821</td>
      <td>2.95288</td>
      <td>0.913</td>
      <td>-18.297</td>
      <td>0.05753</td>
      <td>-5.142</td>
      <td>-60.0</td>
      <td>[0.173, 0.065, 0.242, 0.077, 0.14, 0.228, 0.50...</td>
      <td>[29.171, 56.039, -131.697, 364.537, 31.379, -4...</td>
    </tr>
    <tr>
      <th>450</th>
      <td>129.06236</td>
      <td>2.86077</td>
      <td>0.754</td>
      <td>-26.640</td>
      <td>0.25059</td>
      <td>-15.775</td>
      <td>0.0</td>
      <td>[0.028, 0.009, 0.009, 0.282, 0.011, 0.012, 1.0...</td>
      <td>[41.445, -60.893, 115.289, 22.073, 53.175, -20...</td>
    </tr>
    <tr>
      <th>689</th>
      <td>200.28372</td>
      <td>2.04327</td>
      <td>0.846</td>
      <td>-18.647</td>
      <td>0.10077</td>
      <td>-6.902</td>
      <td>0.0</td>
      <td>[0.014, 0.034, 0.208, 0.031, 0.012, 0.021, 0.0...</td>
      <td>[46.656, -17.364, 60.161, -61.633, 43.313, -13...</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.nlargest(1,['duration'])
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>start</th>
      <th>duration</th>
      <th>confidence</th>
      <th>loudness_start</th>
      <th>loudness_max_time</th>
      <th>loudness_max</th>
      <th>loudness_end</th>
      <th>pitches</th>
      <th>timbre</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>699</th>
      <td>205.36821</td>
      <td>2.95288</td>
      <td>0.913</td>
      <td>-18.297</td>
      <td>0.05753</td>
      <td>-5.142</td>
      <td>-60.0</td>
      <td>[0.173, 0.065, 0.242, 0.077, 0.14, 0.228, 0.50...</td>
      <td>[29.171, 56.039, -131.697, 364.537, 31.379, -4...</td>
    </tr>
  </tbody>
</table>
</div>



#### How many bars are in the song?


```python
len(data['bars'])
```




    103



#### What's the average length of a bar?


```python
import numpy as np
durations = []
for bar in data['bars']:
    durations.append(bar['duration'])
np.mean(durations)
```




    1.9745940776699027



### Save your DataFrame of Segments to a new JSON file using pandas

- Use `df.to_json()` with:
    - The name of new json file. Something like "Data/song_segments.json"
    - Add "orient='records'" to save the data as a list of dictionaries.


```python
df.to_json("Data/song_segments.json", orient='records')
```

#### Use the open function and json module to load in your new json file and preview the first entry.


```python
with open("Data/song_segments.json",'r') as file:
    json_file = file.read()
    data = json.loads(json_file)
data[0]
```




    {'start': 0.0,
     'duration': 0.12186,
     'confidence': 0.0,
     'loudness_start': -60.0,
     'loudness_max_time': 0.0,
     'loudness_max': -60.0,
     'loudness_end': 0.0,
     'pitches': [0.794,
      0.306,
      0.104,
      0.068,
      0.042,
      0.102,
      0.273,
      0.19,
      0.669,
      0.661,
      1.0,
      0.024],
     'timbre': [0.069,
      170.355,
      10.68,
      -30.205,
      57.752,
      -50.964,
      15.234,
      3.391,
      -26.371,
      0.889,
      -8.943,
      -8.084]}


