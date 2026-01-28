**GitHub Remote** 
gitHub repo URL: https://github.com/cs121050/androidApp.JazzLibraryKTRoomJPCompose
reponame:  androidApp.JazzLibraryKTRoomJPCompose
repo HTTPS link: 



---


AI prompts:

gen the room initialisation:
```text
ok!!!! hello hello,, so im back. I have just created my hibernate springboot api and now i am ready for creating the kotlin android app. I will start from 0 first creating the layer that will have the room database. guideme step by step of how to do it starting for zero , add detail.

right nowi have created the empty activity project and i want to start by creating my first entities,, lets start for the entities artist:"package com.nicosarr.jazzLibraryAPI.Artist;
import java.util.ArrayList;
import java.util.List;
import java.util.Objects;
import java.util.stream.Collectors;

import com.fasterxml.jackson.annotation.JsonBackReference;
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;
import com.fasterxml.jackson.annotation.JsonInclude;
import com.fasterxml.jackson.annotation.JsonManagedReference;
import com.fasterxml.jackson.annotation.JsonProperty;
import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlRootElement;

import jakarta.persistence.*;

import com.nicosarr.jazzLibraryAPI.Video.Video;
import com.nicosarr.jazzLibraryAPI.Instrument.Instrument;
import com.nicosarr.jazzLibraryAPI.Quote.Quote;
import com.nicosarr.jazzLibraryAPI.VideoContainsArtist.VideoContainsArtist;

@Entity
@Table(name = "Artist")  // database tables
@JacksonXmlRootElement(localName = "artist")
public class Artist {

	@Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Use IDENTITY if your DB supports auto-increment
    @Column(name = "artist_id")	
    private int artist_id;
	
    @Column(name = "artist_name")
    private String artist_name;
    
    @Column(name = "artist_surname")    
    private String artist_surname;
    
    @Column(name = "artist_rank")    
    private Integer  artist_rank;    
    
    @ManyToOne(fetch = FetchType.LAZY)  // This makes it lazy loaded
    @JoinColumn(
    		name = "instrument_id", 
    		referencedColumnName = "instrument_id", 
    		foreignKey = @ForeignKey(name = "FK_instrument_id")
    )
    @JsonIgnore  // This will exclude instrument from JSON serialization
    private Instrument instrument;  // Change from int to Instrument object
    @Transient
    private int instrument_id; 
        
    @OneToMany(mappedBy = "artist", fetch = FetchType.LAZY)
    private List<VideoContainsArtist> videoContainsArtists = new ArrayList<>();

    @OneToMany(mappedBy = "artist", fetch = FetchType.LAZY)
    private List<Quote> quotes = new ArrayList<>(); 
    
	public Artist() {
	}
    public Artist (int artist_id, String artist_name, String artist_surname, int instrument_id, Integer  artist_rank){
	   	this.artist_id = artist_id;
	   	this.artist_name = artist_name;
	   	this.artist_surname = artist_surname;
	   	this.instrument_id = instrument_id;	   	
	   	this.artist_rank= artist_rank;		   	
    }
    public Artist (String artist_name, String artist_surname, int instrument_id, Integer  artist_rank){
	   	this.artist_name = artist_name;
	   	this.artist_surname = artist_surname;
	   	this.instrument_id = instrument_id;	   	
	   	this.artist_rank= artist_rank;	   		
	   	
    }    
    public Artist (String artist_name, String artist_surname, int instrument_id){
	   	this.artist_name = artist_name;
	   	this.artist_surname = artist_surname;
	   	this.instrument_id = instrument_id;	   	
	   	this.artist_rank= 0;		
    }      
    
    public int getArtist_id() {
        return artist_id;
    }
    public void setArtist_id(int artist_id) {
        this.artist_id = artist_id;
    }
    public String getArtist_name() {
        return artist_name;
    }
    public void setArtist_name(String artist_name) {
        this.artist_name = artist_name;
    }
    public String getArtist_surname() {
        return artist_surname;
    }
    public void setArtist_surname(String artist_surname) {
        this.artist_surname = artist_surname;
    }
	public Instrument getInstrument() {
		return instrument;
	}
	public void setInstrument(Instrument instrument) {
		this.instrument = instrument;
	}
    // Add getter for instrument_id only
    public int getInstrument_id() {
        return this.instrument != null ? this.instrument.getInstrument_id() : 0;
    }
	public void setInstrument_id(int instrument_id) {
		this.instrument_id = instrument_id;
	}
	//@JsonIgnore 
	public List<VideoContainsArtist> getVideoContainsArtists() {
		return videoContainsArtists;
	}
	public void setVideoContainsArtists(List<VideoContainsArtist> videoContainsArtists) {
		this.videoContainsArtists = videoContainsArtists;
	}
	public Integer  getArtist_rank() {
		return artist_rank;
	}
	public void setArtist_rank(Integer  artist_rank) {
		this.artist_rank = artist_rank;
	}
	// Add a transient field to get videos directly
    @Transient
    @JsonProperty("videos") // This will include videos in the JSON
    public List<Video> getVideos() {
        if (videoContainsArtists == null) {
            return new ArrayList<>();
        }
        return videoContainsArtists.stream()
            .map(VideoContainsArtist::getVideo)
            .collect(Collectors.toList());
    }
	   
	public String toString(){
        return "artist_id:" + artist_id + "#artist_name:" + artist_name + "#artist_surname:" + artist_surname 
          + "#instrument_id:" + instrument_id+ "#artist_rank:" + artist_rank;
    }  
    public String valuesToString(){
        return artist_id + "#" + artist_name + "#" + artist_surname + "#" + instrument_id +"#"+artist_rank;
    }        
    public Artist toObject(){
         return new Artist(this.artist_id, this.artist_name, this.artist_surname, this.instrument_id, this.artist_rank);   
    }  
}

",intrument:"package com.nicosarr.jazzLibraryAPI.Instrument;
import java.util.ArrayList;
import java.util.List;

import com.fasterxml.jackson.annotation.JsonBackReference;
import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlRootElement;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.FetchType;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.Table;
import jakarta.persistence.OneToMany;

import com.nicosarr.jazzLibraryAPI.Artist.Artist;

@Entity
@Table(name = "Instrument")  // database tables
@JacksonXmlRootElement(localName = "instrument")
public class Instrument {
    
	@Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Use IDENTITY if your DB supports auto-increment	
    @Column(name = "instrument_id")
	private int instrument_id;
    
    @Column(name = "instrument_name")
	private String instrument_name;

    @OneToMany(mappedBy = "instrument", fetch = FetchType.LAZY)
    @JsonBackReference
    @JsonIgnore
    private List<Artist> artists = new ArrayList<>();
    
	public Instrument () {
	}	
	public Instrument (int instrument_id, String instrument_name){
	   	this.instrument_id = instrument_id;
	   	this.instrument_name = instrument_name;   	
    }
    public Instrument (String instrument_name){
 	   	this.instrument_name = instrument_name;   	
    }     

	public int getInstrument_id() {
		return instrument_id;
	}
	public void setInstrument_id(int instrument_id) {
		this.instrument_id = instrument_id;
	}
	public String getInstrument_name() {
		return instrument_name;
	}
	public void setInstrument_name(String instrument_name) {
		this.instrument_name = instrument_name;
	}
    public List<Artist> getArtists() {
        return artists;
    }
    public void setArtists(List<Artist> artists) {
        this.artists = artists;
    }
}

",quote:"package com.nicosarr.jazzLibraryAPI.Quote;


import java.util.ArrayList;

import com.fasterxml.jackson.annotation.JsonIgnore;
import com.fasterxml.jackson.dataformat.xml.annotation.JacksonXmlRootElement;
import com.nicosarr.jazzLibraryAPI.Artist.Artist;
import com.nicosarr.jazzLibraryAPI.Instrument.Instrument;
import com.fasterxml.jackson.annotation.JsonProperty;

import jakarta.persistence.Column;
import jakarta.persistence.Entity;
import jakarta.persistence.FetchType;
import jakarta.persistence.ForeignKey;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.ManyToOne;
import jakarta.persistence.Table;
import jakarta.persistence.Transient;


@Entity
@Table(name = "Quote")  // database tables
@JacksonXmlRootElement(localName = "quote")
public class Quote {

	@Id
    @GeneratedValue(strategy = GenerationType.IDENTITY) // Use IDENTITY if your DB supports auto-increment	
	private int quote_id;
    @Column(name = "quote_text")	
    private String quote_text;
    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(
    		name = "artist_id", 
    		referencedColumnName = "artist_id", 
    		foreignKey = @ForeignKey(name = "FK_artist_id")
    )
    @JsonIgnore 
    private Artist artist; 
    @Transient
    private int artist_id; 

	public Quote () {
	}
    public Quote(int quote_id, String quote_text, int artist_id) {
        this.quote_id = quote_id;
        this.quote_text = quote_text;
        this.artist_id = artist_id;
    }
    public Quote(String quote_text, int artist_id) {
        this.quote_text = quote_text;
        this.artist_id = artist_id;
    }
    public Quote(String quote_text) {
        this.quote_text = quote_text;
        this.artist_id = 0;
    }    
    public String getQuote_text() {
		return quote_text;
	}
	public void setQuote_text(String quote_text) {
		this.quote_text = quote_text;
	}
	public int getQuote_id() {
		return quote_id;
	}
	public void setQuote_id(int quote_id) {
		this.quote_id = quote_id;
	}
    // Add getter for instrument_id only
    public int getArtist_id() {
        return this.artist != null ? this.artist.getArtist_id() : 0;
    }
	public void setArtist_id(int artist_id) {
		this.artist_id = artist_id;
	}

	public String toString(){
        return "quote_id:" + quote_id + "#quote_text:" + quote_text + "#artist_id:" + artist_id;
    }   
    public String valuesToString(){
        return quote_id + "#" + quote_text + "#" + artist_id + "#";
    }      
    public Quote toObject(){
        return new Quote(this.quote_id, this.quote_text, this.artist_id);          
    }

}
    
	
". Start of creating the directory tree for room
```


steps to create the android project :

libs.versions.toml
```toml
[versions]  
# This table defines version numbers for all dependencies, ensuring consistent versioning across the project.  
# Each key represents a dependency, and its value is the specific version string to be used.  
agp = "8.6.1"                     # Android Gradle Plugin version for building Android applications  
kotlin = "1.9.23"                 # Kotlin programming language version  
coreKtx = "1.12.0"                # AndroidX Core KTX extension library version  
junit = "4.13.2"                  # JUnit 4 testing framework version  
junitVersion = "1.1.5"            # AndroidX JUnit extension version for instrumentation tests  
espressoCore = "3.5.1"            # Espresso UI testing framework version  
lifecycleRuntimeKtx = "2.6.2"     # Lifecycle runtime KTX extensions version  
activityCompose = "1.8.2"         # Jetpack Compose Activity integration version  
composeBom = "2023.10.01"         # Compose Bill of Materials (BOM) version to manage Compose library versions  
room = "2.6.1"                    # Room persistence library version for SQLite database abstraction  
coroutines = "1.7.3"              # Kotlin Coroutines version for asynchronous programming  
material3 = "1.1.2"               # Material Design 3 components for Jetpack Compose version  
  
[libraries]  
# This table defines library dependencies referenced by alias, specifying group, name, and version reference.  
# Each entry creates a reusable alias for a specific library dependency.  
androidx-core-ktx = { group = "androidx.core", name = "core-ktx", version.ref = "coreKtx" }                # Core KTX extensions for Android framework APIs  
junit = { group = "junit", name = "junit", version.ref = "junit" }                                         # JUnit 4 testing framework  
androidx-junit = { group = "androidx.test.ext", name = "junit", version.ref = "junitVersion" }             # AndroidX JUnit extensions for instrumentation tests  
androidx-espresso-core = { group = "androidx.test.espresso", name = "espresso-core", version.ref = "espressoCore" } # Espresso UI testing framework  
androidx-lifecycle-runtime-ktx = { group = "androidx.lifecycle", name = "lifecycle-runtime-ktx", version.ref = "lifecycleRuntimeKtx" } # Lifecycle runtime KTX extensions  
androidx-activity-compose = { group = "androidx.activity", name = "activity-compose", version.ref = "activityCompose" } # Compose integration with Activity  
androidx-compose-bom = { group = "androidx.compose", name = "compose-bom", version.ref = "composeBom" }               # Compose BOM to manage Compose library versions  
androidx-ui = { group = "androidx.compose.ui", name = "ui" }                                                     # Compose UI foundational components  
androidx-ui-graphics = { group = "androidx.compose.ui", name = "ui-graphics" }                                   # Compose graphics and drawing APIs  
androidx-ui-tooling = { group = "androidx.compose.ui", name = "ui-tooling" }                                     # Compose tooling support for previews  
androidx-ui-tooling-preview = { group = "androidx.compose.ui", name = "ui-tooling-preview" }                     # Compose preview annotations and tooling  
androidx-ui-test-manifest = { group = "androidx.compose.ui", name = "ui-test-manifest" }                         # Test manifest for Compose UI tests  
androidx-ui-test-junit4 = { group = "androidx.compose.ui", name = "ui-test-junit4" }                             # JUnit 4 integration for Compose UI tests  
androidx-material3 = { group = "androidx.compose.material3", name = "material3", version.ref = "material3" }     # Material Design 3 components for Compose  
  
# Add these Room dependencies  
androidx-room-runtime = { group = "androidx.room", name = "room-runtime", version.ref = "room" }             # Room runtime library for database operations  
androidx-room-ktx = { group = "androidx.room", name = "room-ktx", version.ref = "room" }                     # Room KTX extensions for Coroutines support  
androidx-room-compiler = { group = "androidx.room", name = "room-compiler", version.ref = "room" }           # Room annotation processor for code generation  
  
# Add Coroutines  
kotlinx-coroutines-android = { group = "org.jetbrains.kotlinx", name = "kotlinx-coroutines-android", version.ref = "coroutines" } # Kotlin Coroutines for Android  
  
[plugins]  
# This table defines Gradle plugins with their IDs and version references.  
android-application = { id = "com.android.application", version.ref = "agp" }             # Android application plugin for building APKs  
kotlin-android = { id = "org.jetbrains.kotlin.android", version.ref = "kotlin" }         # Kotlin Android plugin for Kotlin support  
kotlin-kapt = { id = "org.jetbrains.kotlin.kapt" }                                       # Kotlin annotation processing tool (kapt) plugin
```
example.JazzLibraryKTRoomJPCompose

build.gradle.kts (module::app?)
```kts
// This is the main module-level Gradle build configuration file (build.gradle.kts).  
// It configures the Android application plugin, defines build settings (compileSdk, namespace, etc.),  
// and declares all dependencies for the project using the version catalog from libs.versions.toml.  
plugins {  
    alias(libs.plugins.android.application)  // Apply the Android application plugin for building Android apps  
    alias(libs.plugins.kotlin.android)       // Apply the Kotlin Android plugin for Kotlin language support  
    id("kotlin-kapt")                        // Apply the Kotlin annotation processor plugin for Room  
}  
  
android {  
    namespace = "com.example.jazzlibraryktroomjpcompose"  // Unique namespace for the application  
    compileSdk = 34                                         // Compile against Android API level 34  
  
    defaultConfig {  
        applicationId = "com.example.jazzlibraryktroomjpcompose"  // Package name for the app  
        minSdk = 26                                               // Minimum Android API level supported  
        targetSdk = 34                                            // Target Android API level for optimizations  
        versionCode = 1                                           // Internal version number for updates  
        versionName = "1.0"                                       // User-visible version name  
  
        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"  // Test runner for instrumentation tests  
        vectorDrawables {  
            useSupportLibrary = true  // Enable vector drawable support for older APIs  
        }  
    }  
    buildTypes {  
        release {  
            isMinifyEnabled = false  // Disable code shrinking for release (can be enabled for production)  
            proguardFiles(  
                getDefaultProguardFile("proguard-android-optimize.txt"),  // Default Android ProGuard rules  
                "proguard-rules.pro"                                       // Custom ProGuard rules for the project  
            )  
        }  
    }    compileOptions {  
        sourceCompatibility = JavaVersion.VERSION_17  // Java 17 source compatibility  
        targetCompatibility = JavaVersion.VERSION_17  // Java 17 bytecode target  
    }  
    kotlinOptions {  
        jvmTarget = "17"  // Target JVM 17 for Kotlin compilation  
    }  
    buildFeatures {  
        compose = true     // Enable Jetpack Compose for UI  
        buildConfig = true // Enable generated BuildConfig class  
    }  
    composeOptions {  
        kotlinCompilerExtensionVersion = "1.5.11"  // Kotlin compiler extension version for Compose  
    }  
    packaging {  
        resources {  
            excludes += "/META-INF/{AL2.0,LGPL2.1}"  // Exclude duplicate license files from packaging  
        }  
    }}  
  
dependencies {  
    implementation(libs.androidx.core.ktx)                    // Core KTX extensions for Android framework  
    implementation(libs.androidx.lifecycle.runtime.ktx)       // Lifecycle runtime KTX extensions  
    implementation(libs.androidx.activity.compose)            // Compose integration with Activity  
    implementation(platform(libs.androidx.compose.bom))       // Compose BOM for version management  
    implementation(libs.androidx.ui)                          // Compose UI foundational components  
    implementation(libs.androidx.ui.graphics)                 // Compose graphics and drawing APIs  
    implementation(libs.androidx.ui.tooling.preview)          // Compose preview tooling support  
    implementation(libs.androidx.material3)                   // Material Design 3 components for Compose  
  
    // Room Database    implementation(libs.androidx.room.runtime)               // Room runtime for database operations  
    implementation(libs.androidx.room.ktx)                   // Room KTX extensions for Coroutines  
    kapt(libs.androidx.room.compiler)                        // Room annotation processor for code generation  
  
    // Coroutines    implementation(libs.kotlinx.coroutines.android)          // Kotlin Coroutines for Android  
  
    testImplementation(libs.junit)                           // JUnit 4 for unit tests  
    androidTestImplementation(libs.androidx.junit)           // AndroidX JUnit extensions for instrumented tests  
    androidTestImplementation(libs.androidx.espresso.core)   // Espresso for UI tests  
    androidTestImplementation(platform(libs.androidx.compose.bom))  // Compose BOM for Android tests  
    androidTestImplementation(libs.androidx.ui.test.junit4)  // Compose UI testing JUnit 4 integration  
    debugImplementation(libs.androidx.ui.tooling)            // Compose tooling for debug builds  
    debugImplementation(libs.androidx.ui.test.manifest)      // Test manifest for Compose UI tests in debug  
}
```


my initial .gitignore
```
*.iml
.gradle
/local.properties
/.idea/caches
/.idea/libraries
/.idea/modules.xml
/.idea/workspace.xml
/.idea/navEditor.xml
/.idea/assetWizardSettings.xml
.DS_Store
/build
/captures
.externalNativeBuild
.cxx
local.properties

```




the DATA layer ARCHITECTURE
```
app/src/main/java/com/nicosarr/jazzLibraryAPI/
├── data/                              # ⭐ DATA LAYER ⭐
│   │                                   # How data is fetched/stored
│   │                                   # Contains implementations, adapters, mappers
│   │                                   # Depends on: Domain layer ONLY
│   │
│   ├── local/                         # 📍 LOCAL DATA SOURCES
│   │   │                               # Everything related to local storage
│   │   │                               # Room database, SharedPreferences, DataStore
│   │   │
│   │   ├── entities/                  # 🗄️ ROOM ENTITIES
│   │   │   │                           # Database table definitions
│   │   │   │                           # Annotated with @Entity for Room
│   │   │   │                           # Maps database rows to objects
│   │   │   │                           # Example: ArtistEntity.kt
│   │   │   ├── ArtistEntity.kt        #   ↔️ Database table "artists"
│   │   │   ├── InstrumentEntity.kt    #   ↔️ Database table "instruments"
│   │   │   └── QuoteEntity.kt         #   ↔️ Database table "quotes"
│   │   │
│   │   ├── daos/                      # 🛠️ DATA ACCESS OBJECTS
│   │   │   │                           # Room DAO interfaces
│   │   │   │                           # Annotated with @Dao
│   │   │   │                           # Contains SQL queries for CRUD operations
│   │   │   │                           # Example: ArtistDao.kt
│   │   │   ├── ArtistDao.kt           #   📋 SQL queries for artists table
│   │   │   ├── InstrumentDao.kt       #   📋 SQL queries for instruments table
│   │   │   └── QuoteDao.kt            #   📋 SQL queries for quotes table
│   │   │
│   │   └── JazzDatabase.kt            # 🗃️ ROOM DATABASE
│   │                                   # Main database class
│   │                                   # Extends RoomDatabase
│   │                                   # Lists all entities and DAOs
│   │                                   # Singleton pattern for DB instance
│   │
│   ├── remote/                        # 📡 REMOTE DATA SOURCES
│   │   │                               # Everything related to network/API
│   │   │                               # Retrofit, OkHttp, API services
│   │   │
│   │   ├── api/                       # 🌐 API INTERFACES
│   │   │   │                           # Retrofit service interfaces
│   │   │   │                           # Define HTTP endpoints
│   │   │   │                           # Annotated with @GET, @POST, etc.
│   │   │   └── JazzApiService.kt      #   🔌 Contract for Spring Boot API endpoints
│   │   │
│   │   ├── models/                    # 📦 API RESPONSE MODELS
│   │   │   │                           # Data classes matching API JSON responses
│   │   │   │                           # Annotated with @SerializedName for Gson
│   │   │   │                           # Maps JSON → Kotlin objects
│   │   │   ├── ArtistResponse.kt      #   🎯 JSON response for /api/artists
│   │   │   ├── InstrumentResponse.kt  #   🎯 JSON response for /api/instruments
│   │   │   └── QuoteResponse.kt       #   🎯 JSON response for /api/quotes
│   │   │
│   │   └── RetrofitClient.kt          # 🔗 RETROFIT CLIENT
│   │                                   # Singleton Retrofit instance
│   │                                   # Configured with base URL, interceptors
│   │                                   # Creates API service implementations
│   │
│   └── repository/                    # ⚡ REPOSITORY IMPLEMENTATIONS
│       │                               # CONCRETE implementations of domain repositories
│       │                               # Coordinates between local and remote sources
│       │                               # Contains data orchestration logic
│       │                               # Implements: Domain repository interfaces
│       │
│       └── ArtistRepositoryImpl.kt    #   🎭 Implements ArtistRepository interface
│                                       #   📞 Calls: LocalDataSource + RemoteDataSource
│                                       #   🔀 Decides: Cache-first vs Network-first
│                                       #   🔄 Handles: Data transformation & sync
│
├── domain/                            # ⭐ DOMAIN LAYER ⭐
│   │                                   # Pure business logic (NO Android dependencies!)
│   │                                   # Independent of frameworks, UI, databases
│   │                                   # Contains: Models, Repository interfaces, UseCases
│   │                                   # Can be reused in other platforms (KMM, backend)
│   │
│   ├── models/                        # 🏛️ DOMAIN MODELS
│   │   │                               # Core business entities
│   │   │                               # Pure data classes (no annotations!)
│   │   │                               # Used throughout the app (UI, business logic)
│   │   │                               # NEVER contain Android/JVM-specific code
│   │   │
│   │   ├── Artist.kt                  #   🎷 Core Artist business entity
│   │   ├── Instrument.kt              #   🎺 Core Instrument business entity
│   │   └── Quote.kt                   #   💬 Core Quote business entity
│   │
│   ├── repository/                    # 📜 REPOSITORY INTERFACES
│   │   │                               # ABSTRACT contracts for data operations
│   │   │                               # Define WHAT can be done (not HOW)
│   │   │                               # Implemented by data layer
│   │   │                               # Used by use cases and view models
│   │   │
│   │   └── ArtistRepository.kt        #   📋 Contract for artist operations
│   │                                   #   Example methods: getArtists(), saveArtist()
│   │                                   #   Pure interface - no implementation here!
│   │
│   └── usecases/                      # 🎯 USE CASES (Interactors)
│       │                               # Single business operations
│       │                               # Each use case does ONE specific thing
│       │                               // 🎭 EXAMPLE: GetArtistsUseCase
│       │                               // 1. Orchestrates data flow: Repository → Domain Model
│       │                               // 2. Contains business rules/validation
│       │                               // 3. Can combine multiple repository calls
│       │                               // 4. Easily testable (no Android dependencies)
│       │                               // 5. Reusable across different ViewModels
│       │
│       ├── GetArtistsUseCase.kt       #   📋 Use case: "Get all artists"
│       ├── GetArtistByIdUseCase.kt    #   📋 Use case: "Get artist by ID"
│       └── RefreshArtistsUseCase.kt   #   📋 Use case: "Refresh artists from API"
│                                       // 🔄 FLOW: ViewModel → UseCase → Repository → Data
│
└── presentation/                      # ⭐ PRESENTATION LAYER ⭐
    │                                   // Everything UI-related
    │                                   // Depends on: Domain layer
    │                                   // Contains: ViewModels, UI components, navigation
    │                                   // Android framework specific (Activities, Fragments)
    │
    ├── viewmodels/                    // 🧠 VIEW MODELS
    │   │                               // Bridge between UI and business logic
    │   │                               // Extends AndroidViewModel or ViewModel
    │   │                               // Holds UI state, handles user interactions
    │   │                               // NEVER contains Android Views/Context!
    │   │                               // Communicates with: UseCases only!
    │   │
    │   └── ArtistViewModel.kt         //   🎨 ViewModel for artist-related UI
    │                                   //   📊 Holds: artists list, loading state, errors
    │                                   //   🎯 Calls: UseCases for business logic
    │                                   //   🔄 Exposes: LiveData/StateFlow to UI
    │                                   //   🎭 Example: fun loadArtists() { useCase() }
    │
    └── ui/                            // 🎨 UI COMPONENTS
        │                               // Activities, Fragments, Composable functions
        │                               // XML layouts, Jetpack Compose
        │                               // Observes: ViewModel state
        │                               // Handles: User input, navigation
        │                               // NEVER contains business logic!
        │
        ├── artists/                   //   📋 Screen: Artist list
        │                               //   Files: ArtistsFragment.kt, artists_fragment.xml
        │                               //   Shows: List of all artists
        │                               //   Actions: Click → Artist detail
        │
        └── artistdetail/              //   📋 Screen: Artist details
                                        //   Files: ArtistDetailFragment.kt, detail_fragment.xml
                                        //   Shows: Single artist + quotes
                                        //   Actions: Edit, Delete, Share
```



## Back end testing Screens logic 

- [ ] **Testing screen :** when the app starts the first screen has a list of buttons, each button is an activity, this app will redirect to the chosen activity: **mainActivityTestRoom**, **mainActivityTestRoomFilters**, **mainActivityTestRoomRetrofit**, **mainActivityTestRoomRetrofitFilters**. And finally once the backend work as expected, create the functional ui of the app.
- [ ] 





## the order of dev, in order to create a new Table

Step 1: Create Domain Models First(domain/models/Video.kt)
Step 2: Create Room Entities(data/local/entities/VideoEntity.kt)
Step 3: Create DAOs (Data Access Objects) (data/local/daos/VideoDao.kt)
Step 4: Update Your Database Class(JazzDatabase.kt)
Step 5: Create Mappers(data/mappers/VideoMapper.kt)
Step 6: Create Repository Interfaces (domain/repository/VideoRepository.kt) 
step7: Step 7: Create Repository Implementation(data/repository/VideoRepositoryImpl.kt)
Step 8: Update DI Module(AppModule.kt)
Step 11: Update Your UI for Testing(Add new tabs to your test screen:)









## Future Upgrades

- [ ] at Quote table add the Video_id column, so to relate the video from witch the quote was diarived: 1) change API structure, set it to FK NULLable 1.2) Test 1.3) Deploy and test 1.4) in android app, add the new column... test in
- [ ] get books of interviews of jazz musicians, get them to ai to read them, and get AI produse a video of the actual interview with generated people talking... This way we will three-fold the content of the app, and the knowledge inside. ALSO this will AUTOMATE the prosess ofpopulating thedata with media... mannualy adding youtube-urls will stop!!! **Amazing revenue possibilities**
- [ ] Quote Reading Mode! : with a button you will access a quote reading activity with lists of quotes , there each quote will be in a list, from each item u will have the option to redirect to the video witch this quote got originated, if the quote.video_id!=NULL a video icon will be visible near the list AND the redirrection will be possible, ELSE message:: this link is not linked with a Media. **Other filtering filtering options:**  all the pree existing filtering UI will be available... but filters 'duration', and 'type' will be unavailable. (actualy ,,, filter duration could replaised with 'Length'-> 0to10 Words, 10to20 Words, 20to30Words, 30toMore).
	- [ ] make sure the name of the artist can be searched both nameSurename AND surnameName.
- [ ] **The search bar behaivio**r: the search bar will be searching the String this way '%Srting%' at BOTH 'artist' and 'Video' tables taking in acound the already selected filters, for strarting, lets asumed no filters are pre selected. When the string match some video.video_name OR artist.artist_fullName a scrollable drop down will be apearing. The dropdown will be splited to 2 scrollable linear views, one for the artists, one for the videos. the video.video_name and artist.artist_fullName will appear uncut expanding to multiple lines in case it doesn't fit the layout. Also an icon/ emoji can shown at the start of the name string to indicate the nature of the representative item. When the user chose an artist item then the artist filter will be chosen automaticaly as the user chosed it from the filter view. If the user chose the video item, then then the video's artist will be chosen in the filter path, that naturaly results to the retrieving of the VideoItems related with the filterpath, the algorithm will make sure the selected video item from the dropdownmanue will beremovedby the result set and pined at the top of the videoPlayer  list, make sure that when you are refreasing the feed, the pinnedvideo staing! **In the case you are accesing the search bar while a filter path is selected** then the search will only accure at the video or arist exist in the determined of the filter path resut set. (you can attach at the end of the query SQL an 'extraWhere' that contain the constrains of the filterpath). In case artist filter is choosed the search will only happen for videos. In case duration path is selected the search will conserne only the videos having the same video.video_duration. **In case you change the searching option to 'Quote'** the drop down layout will change, now it will show only on linear layout , each item will contain three items: The query's part where the searched text appearing, the artist_name and the video_name that this specific quote is apearing. (possibly make the query item scrollable so to beable to read the whole quote, the searched subText will apear bold! )
- [ ] **create AI compression**: force ai to create a syntax of prdicting the compressed word: first compress the characters using AI, then ask ai to compress the text, and then de compress it. First you need to studdie the Logic of compresion.





promts 


also i want you to generate those queries in the DAO class that sutisfy the usecase i have made : 

typeDao: 1.1)getTypeById 1.2) getTypeByName, 2.1)