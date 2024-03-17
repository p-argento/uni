Column description tracks.csv

- id: 				The Spotify ID for the track
- name: 			Name of the track
- duration_ms: 			The track length in milliseconds
- explicit: 			Whether or not the track has explicit lyrics (true = yes it does; false = no it does not OR unknown)
- popularity: 			The popularity of a track is a value between 0 and 100, with 100 being the most popular. The popularity is calculated 
					by algorithm and is based, in the most part, on the total number of plays the track has had and how recent 
					those plays are. Generally speaking, songs that are being played a lot now will have a higher popularity 
					than songs that were played a lot in the past. Duplicate tracks (e.g. the same track from a single and an album) 
					are rated independently. Artist and album popularity is derived mathematically from track popularity.
- artists: 			The artists' names who performed the track. If there is more than one artist, they are separated by a ;
- album_type
- album_name: 	 		The album name in which the track appears
- danceability: 		Danceability describes how suitable a track is for dancing based on a combination of musical elements including tempo, 
					rhythm stability, beat strength, and overall regularity. A value of 0.0 is least danceable and 1.0 is most danceable    
- energy: 			Energy is a measure from 0.0 to 1.0 and represents a perceptual measure of intensity and activity. Typically, energetic 
					tracks feel fast, loud, and noisy. For example, death metal has high energy, while a Bach prelude scores low on the scale
- key:				The key the track is in. Integers map to pitches using standard Pitch Class notation. 
					E.g. 0 = C, 1 = C♯/D♭, 2 = D, and so on. If no key was detected, the value is -1
- loudness: 			The overall loudness of a track in decibels (dB)
- mode:				Mode indicates the modality (major or minor) of a track, the type of scale from which its melodic content is derived. 
					Major is represented by 1 and minor is 0
- speechiness: 			Speechiness detects the presence of spoken words in a track. The more exclusively speech-like the 
					recording (e.g. talk show, audio book, poetry), the closer to 1.0 the attribute value. Values above 0.66
					describe tracks that are probably made entirely of spoken words. Values between 0.33 and 0.66 describe
					tracks that may contain both music and speech, either in sections or layered, including such cases as rap music. 
					Values below 0.33 most likely represent music and other non-speech-like tracks
- acousticness:			A confidence measure from 0.0 to 1.0 of whether the track is acoustic. 1.0 represents high confidence the track is acoustic
- instrumentalness:		Predicts whether a track contains no vocals. "Ooh" and "aah" sounds are treated as instrumental in this context. 
					Rap or spoken word tracks are clearly "vocal". The closer the instrumentalness value is to 1.0, 
					the greater likelihood the track contains no vocal content
- liveness:			Detects the presence of an audience in the recording. Higher liveness values represent an increased probability that 
					the track was performed live. A value above 0.8 provides strong likelihood that the track is live
- valence:			A measure from 0.0 to 1.0 describing the musical positiveness conveyed by a track. 
					Tracks with high valence sound more positive (e.g. happy, cheerful, euphoric), while tracks with low valence sound more
					negative (e.g. sad, depressed, angry)
- tempo:			The overall estimated tempo of a track in beats per minute (BPM). In musical terminology, tempo is the speed or 
					pace of a given piece and derives directly from the average beat duration
- features_duration_ms: 	The duration of the track in milliseconds
- time_signature:		An estimated time signature. The time signature (meter) is a notational convention to specify how many beats 
					are in each bar (or measure). The time signature ranges from 3 to 7 indicating time signatures of 3/4, to 7/4.
- n_beats:			The total number of time intervals of beats throughout the track. A beat is the basic time unit of a piece of music; 
					for example, each tick of a metronome.
- n_bars:			The total number of time intervals of the bars throughout the track. A bar (or measure) is a segment of time defined
					as a given number of beats.
- popularity_confidence: 	The confidence, from 0.0 to 1.0, of the popularity of the song.
- processing: 			Major/minor mode ration aggregated by key.
- genre:			The genre in which the track belongs
- disc_number:			The disc number (usually 1 unless the album consists of more than one disc).
- track_number: 		The number of the track. If an album has several discs, the track number is the number on the specified disc.
- album_type:			The type of the album on which the track appears. Allowed values: "album", "single", "compilation"
- album_release_date: 		The date the album was first released.
- album_release_date_precision:	The precision with which release_date value is known. Allowed values: "year", "month", "day"
- album_total_tracks: 		The number of tracks in the album.
- start_of_fade_out: 		The time, in seconds, at which the track's fade-out period starts. If the track has no fade-out, this should match the track's length.
- tempo_confidence: 		The confidence, from 0.0 to 1.0, of the reliability of the tempo.
- time_signature_confidence: 	The confidence, from 0.0 to 1.0, of the reliability of the time_signature. Sections with time signature changes may correspond to low values in this field.
- key_confidence: 		The confidence, from 0.0 to 1.0, of the reliability of the key. Songs with many key changes may correspond to low values in this field.
- mode_confidence: 		The confidence, from 0.0 to 1.0, of the reliability of the mode.
- n_beats: 			The total number of time intervals of beats throughout the track. A beat is the basic time unit of a piece of music; for example, each tick of a metronome.
- n_bars: 			The total number of time intervals of the bars throughout the track. A bar (or measure) is a segment of time defined as a given number of beats.

Column description artists.csv

- id:  			The Spotify ID for the artist.
- name: 		The name of the artist.
- popularity: 		The popularity of the artist. The value will be between 0 and 100, with 100 being the most popular. The artist's popularity is calculated from the popularity of all the artist's tracks.
- followers:		Information about the followers of the artist.
- genres: 		A list of the genres the artist is associated with. If not yet classified, the array is empty.


