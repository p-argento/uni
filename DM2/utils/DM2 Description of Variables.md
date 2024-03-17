## Column description tracks.csv


| unique | almost unique | binary   | categorical | continuous  |
| ------ | ------------- | -------- | ----------- | ----------- |
| id     |               |          |             |             |
|        | name          |          |             |             |
|        |               |          |             | duration_ms |
|        |               | explicit |             |             |
|        |               |          |             | popularity  |
|        | artists       |          |             |             |
|        |               |          | album_type  |             |
|        | album_name    |          |             |             |
|        |               |          |             |             |



1. id:
	1. The Spotify ID for the track
2. name: 
	1. Name of the track
3. duration_ms:
	1. The track length in milliseconds
4. explicit:
	1. Whether or not the track has explicit lyrics (true = yes it does; false = no it does not OR unknown)
5. popularity: 		The popularity of a track is a value between 0 and 100, with 100 being the most popular. The popularity is calculated 
					1. by algorithm and is based, in the most part, on the total number of plays the track has had and how recent 
					1. those plays are. Generally speaking, songs that are being played a lot now will have a higher popularity 
					1. than songs that were played a lot in the past. Duplicate tracks (e.g. the same track from a single and an album) 
					1. are rated independently. Artist and album popularity is derived mathematically from track popularity.
6. artists: 			The artists' names who performed the track. If there is more than one artist, they are separated by a ;
7. album_type: `['album', 'single', 'compilation']`
8. album_name: 	 		The album name in which the track appears
9. danceability: 		Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, 
					1. rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable    
10. energy: 			Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic 
					1. tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale
11. key:				The key the track is in. Integers map to pitches using standard Pitch Class notation. 
					1. E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on. If no key was detected, the value is -1
12. loudness: 			The overall loudness of a track in decibels (dB)
13. mode:				Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. 
					1. Major is represented by 1 and minor is 0
14. speechiness: 			Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the 
					1. recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66
					1. describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe
					1. tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. 
					1. Values below 0.33 most likely represent music and other non-speech-like tracks
15. acousticness:			A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic
16. instrumentalness:		Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. 
					1. Rap or spoken word tracks are clearly "vocal". The closer the instrumentalness value is to 1.0, 
					1. the greater likelihood the track contains no vocal content
17. liveness:			Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that 
					1. the track was performed live. A value above 0.8 provides strong likelihood that the track is live
18. valence:			A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. 
					1. Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more
					1. negative (e.g. sad, depressed, angry)
19. tempo:			The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or 
					1. pace of a given piece and derives directly from the average beat duration
20. features_duration_ms: 	The duration of the track in milliseconds
21. time_signature:		An estimated time signature. The time signature (meter) is a notational convention to specify how many beats 
					1. are in each bar (or measure). The time signature ranges from 3 to 7 indicating time signatures of 3/4, to 7/4.
22. n_beats:			The total number of time intervals of beats throughout the track. A beat is the basic time unit of a piece of music; 
					1. for example, each tick of a metronome.
23. n_bars:			The total number of time intervals of the bars throughout the track. A bar (or measure) is a segment of time defined
					1. as a given number of beats.
24. popularity_confidence: 	The confidence, from 0.0 to 1.0, of the popularity of the song.
25. processing: 			Major/minor mode ration aggregated by key.
26. genre:			The genre in which the track belongs
27. disc_number:			The disc number (usually 1 unless the album consists of more than one disc).
28. track_number: 		The number of the track. If an album has several discs, the track number is the number on the specified disc.
29. album_type:			The type of the album on which the track appears. Allowed values: "album", "single", "compilation"
30. album_release_date: 		The date the album was first released.
31. album_release_date_precision:	The precision with which release_date value is known. Allowed values: "year", "month", "day"
32. album_total_tracks: 		The number of tracks in the album.
33. start_of_fade_out: 		The time, in seconds, at which the track's fade-out period starts. If the track has no fade-out, this should match the track's length.
34. tempo_confidence: 		The confidence, from 0.0 to 1.0, of the reliability of the tempo.
35. time_signature_confidence: 	The confidence, from 0.0 to 1.0, of the reliability of the time_signature. Sections with time signature changes may correspond to low values in this field.
36. key_confidence: 		The confidence, from 0.0 to 1.0, of the reliability of the key. Songs with many key changes may correspond to low values in this field.
37. mode_confidence: 		The confidence, from 0.0 to 1.0, of the reliability of the mode.
38. n_beats: 			The total number of time intervals of beats throughout the track. A beat is the basic time unit of a piece of music; for example, each tick of a metronome.
39. n_bars: 			The total number of time intervals of the bars throughout the track. A bar (or measure) is a segment of time defined as a given number of beats.

## Column description artists.csv

- id:  			The Spotify ID for the artist.
- name: 		The name of the artist.
- popularity: 		The popularity of the artist. The value will be between 0 and 100, with 100 being the most popular. The artist's popularity is calculated from the popularity of all the artist's tracks.
- followers:		Information about the followers of the artist.
- genres: 		A list of the genres the artist is associated with. If not yet classified, the array is empty.


