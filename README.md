# OctopusFrameworkLibs
#https://github.com/zhuchao-octopus/OctopusFrameworkLibs.git
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////// 
 第一步： 指定依赖的仓库的位置：修改项目的 Gradle  如下：
 
   buildscript {

    repositories {
        google()
        jcenter()
        maven { url 'https://raw.githubusercontent.com/zhuchao-octopus/OctopusFrameworkLibs/master' } //OPlayer 播放器的依赖的位置
    }
    dependencies {
        classpath 'com.android.tools.build:gradle:3.5.0-alpha06'

        // NOTE: Do not place your application dependencies here; they belong
        // in the individual module build.gradle files
    }
}

allprojects {
    repositories {
        google()
        jcenter()
        maven { url 'https://raw.githubusercontent.com/zhuchao-octopus/OctopusFrameworkLibs/master'} //OPlayer 播放器的依赖的位置
    }
}

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
 第二步： 引入依赖：修改模块的 Gradle  如下：
 dependencies {
    implementation fileTree(include: ['*.jar'], dir: 'libs')
    implementation 'com.android.support:leanback-v17:28.0.0'
    implementation 'com.google.code.gson:gson:2.8.5'                 //OPlayer 播放器必须的依赖
    implementation 'com.github.bumptech.glide:glide:3.8.0'           //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libDecodeCore:2.0:@aar'      //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libNetUtil:2.0:@aar'         //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libPlayUtil:2.1:@aar'        //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libPlaySession:2.2:@aar'     //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libVideo:1.0:@aar'           //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libDialog:1.0:@aar'          //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libCallbackEvent:1.0:@aar'   //OPlayer 播放器必须的依赖
    implementation 'com.zhuchao.android:libFileManager:1.0:@aar'     //OPlayer 播放器必须的依赖
    implementation 'com.nineoldandroids:library:2.4.0'
    implementation 'com.android.support:support-v4:28.0.0'
}

第三步：使用播放器,OPlayer 播放器几乎可以解码所有的格式的 视频、音乐、和图片、包括流媒体

  A:利用 OPlayer  播放单个的视频非常的简单，首先定义
  
    private SurfaceView mSurfaceView;
    private Video video;
	
    video = new Video("http://192.168.5.101/cc.mp4", null, null);//最后一个参数是个回调接口，可以获得播放器进度信息
    video.with(this).playInto(mSurfaceView);
	
  B:利用OPlayer 生成播放列表，OPlayer可以根据网络、本地、USB、FTP、生成复杂的播放列表。
  
    1)创建OPlayerSessionManager会话管理器，一个会话代表一个分类信息，比如本地的音乐，一般是在全局的Application中创建会话（见附件）
	   
	   mSessionManager = new OPlayerSessionManager(this,null,null);
	   //注意：这条语句执行完了OPlayer根据网络、本地、USB、FTP、生成播放列表，最后一个参数是个回调接口，通知播放列表创建完成，
	 如何从 OPlayerSession获得具体播放信息呢？（见附件 MediaLibrary.java） 
	

