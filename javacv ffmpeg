# javacv ffmpeg

## 1. FFmpegFrameGrabber

#### FFmpegFrameGrabber.java

```java
public class FFmpegFrameGrabber extends FrameGrabber {
    private static Exception loadingException = null;
    static Map<Pointer, InputStream> inputStreams;
    static FFmpegFrameGrabber.ReadCallback readCallback;
    static FFmpegFrameGrabber.SeekCallback seekCallback;
    private InputStream inputStream;
    private int maximumSize;
    private AVIOContext avio;
    private String filename;
    private AVFormatContext oc;
    private AVStream video_st;
    private AVStream audio_st;
    private AVCodecContext video_c;
    private AVCodecContext audio_c;
    private AVFrame picture;
    private AVFrame picture_rgb;
    private BytePointer[] image_ptr;
    private Buffer[] image_buf;
    private AVFrame samples_frame;
    private BytePointer[] samples_ptr;
    private Buffer[] samples_buf;
    private BytePointer[] samples_ptr_out;
    private Buffer[] samples_buf_out;
    private AVPacket pkt;
    private AVPacket pkt2;
    private int sizeof_pkt;
    private int[] got_frame;
    private SwsContext img_convert_ctx;
    private SwrContext samples_convert_ctx;
    private int samples_channels;
    private int samples_format;
    private int samples_rate;
    private boolean frameGrabbed;
    private Frame frame;
}
```



#### FrameGrabber.java

```java
public abstract class FrameGrabber implements Closeable {
    public static final List<String> list = new LinkedList(Arrays.asList("DC1394", "FlyCapture", "FlyCapture2", "OpenKinect", "OpenKinect2", "RealSense", "PS3Eye", "VideoInput", "OpenCV", "FFmpeg", "IPCamera"));
    public static final long SENSOR_PATTERN_RGGB = 0L;
    public static final long SENSOR_PATTERN_GBRG = 4294967296L;
    public static final long SENSOR_PATTERN_GRBG = 1L;
    public static final long SENSOR_PATTERN_BGGR = 4294967297L;
    protected int videoStream = -1;
    protected int audioStream = -1;
    protected String format = null;
    protected String videoCodecName = null;
    protected String audioCodecName = null;
    protected int imageWidth = 0;
    protected int imageHeight = 0;
    protected int audioChannels = 0;
    protected FrameGrabber.ImageMode imageMode;
    protected long sensorPattern;
    protected int pixelFormat;
    protected int videoCodec;
    protected int videoBitrate;
    protected int imageScalingFlags;
    protected double aspectRatio;
    protected double frameRate;
    protected FrameGrabber.SampleMode sampleMode;
    protected int sampleFormat;
    protected int audioCodec;
    protected int audioBitrate;
    protected int sampleRate;
    protected boolean triggerMode;
    protected int bpp;
    protected int timeout;
    protected int numBuffers;
    protected double gamma;
    protected boolean deinterlace;
    protected Map<String, String> options;
    protected Map<String, String> videoOptions;
    protected Map<String, String> audioOptions;
    protected Map<String, String> metadata;
    protected Map<String, String> videoMetadata;
    protected Map<String, String> audioMetadata;
    protected int frameNumber;
    protected long timestamp;
    protected int maxDelay;
    private ExecutorService executor;
    private Future<Void> future;
    private Frame delayedFrame;
    private long delayedTime;
}
```



## 2. FFmpegFrameRecorder

#### FFmpegFrameRecorder.java

```java
public class FFmpegFrameRecorder extends FrameRecorder {
    private static Exception loadingException = null;
    static Map<Pointer, OutputStream> outputStreams;
    static FFmpegFrameRecorder.WriteCallback writeCallback;
    private OutputStream outputStream;
    private AVIOContext avio;
    private String filename;
    private AVFrame picture;
    private AVFrame tmp_picture;
    private BytePointer picture_buf;
    private BytePointer video_outbuf;
    private int video_outbuf_size;
    private AVFrame frame;
    private Pointer[] samples_in;
    private BytePointer[] samples_out;
    private PointerPointer samples_in_ptr;
    private PointerPointer samples_out_ptr;
    private BytePointer audio_outbuf;
    private int audio_outbuf_size;
    private int audio_input_frame_size;
    private AVOutputFormat oformat;
    private AVFormatContext oc;
    private AVCodec video_codec;
    private AVCodec audio_codec;
    private AVCodecContext video_c;
    private AVCodecContext audio_c;
    private AVStream video_st;
    private AVStream audio_st;
    private SwsContext img_convert_ctx;
    private SwrContext samples_convert_ctx;
    private int samples_channels;
    private int samples_format;
    private int samples_rate;
    private AVPacket video_pkt;
    private AVPacket audio_pkt;
    private int[] got_video_packet;
    private int[] got_audio_packet;
    private AVFormatContext ifmt_ctx;
}
```

#### FrameRecorder.java

```java
public abstract class FrameRecorder implements Closeable {
    public static final List<String> list = new LinkedList(Arrays.asList("FFmpeg", "OpenCV"));
    protected String format;
    protected String videoCodecName;
    protected String audioCodecName;
    protected int imageWidth;
    protected int imageHeight;
    protected int audioChannels;
    protected int pixelFormat;
    protected int videoCodec;
    protected int videoBitrate;
    protected int imageScalingFlags;
    protected int gopSize = -1;
    protected double aspectRatio;
    protected double frameRate;
    protected double videoQuality = -1.0D;
    protected int sampleFormat;
    protected int audioCodec;
    protected int audioBitrate;
    protected int sampleRate;
    protected double audioQuality = -1.0D;
    protected boolean interleaved;
    protected Map<String, String> options = new HashMap();
    protected Map<String, String> videoOptions = new HashMap();
    protected Map<String, String> audioOptions = new HashMap();
    protected Map<String, String> metadata = new HashMap();
    protected Map<String, String> videoMetadata = new HashMap();
    protected Map<String, String> audioMetadata = new HashMap();
    protected int frameNumber = 0;
    protected long timestamp = 0L;
    protected int maxBFrames = -1;
    protected int trellis = -1;
    protected int maxDelay = -1;
}
```

