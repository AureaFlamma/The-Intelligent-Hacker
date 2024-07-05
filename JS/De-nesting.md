Reducing the level of nesting can be achieved by:
- Using an early return 🔴
- Using `async/await` instead of `.then` syntax 🟣
- Using arrow function shorthand without `return` keyword 🟢 
### More complex:
```TS
export const getAspectRatioFromVideo = (video: HTMLVideoElement): AspectRatio => {
  const { videoWidth, videoHeight } = video;
  
  // Finds the greatest common divisor (GCD) using the Euclidean algorithm
  const gcd = (a: number, b: number): number => {
    return b === 0 ? a : gcd(b, a % b);
  };

  if (videoWidth && videoHeight) {
    const divisor = gcd(videoWidth, videoHeight);
    const aspectRatioKey = `${videoWidth / divisor}:${videoHeight / divisor}` as keyof typeof AspectRatio;

    if (AspectRatio[aspectRatioKey]) {
      return AspectRatio[aspectRatioKey];
    }
  }

  return AspectRatio['16:9'];
};
```
### Less complex:
```TS
export const getAspectRatioFromVideo = (video: HTMLVideoElement): AspectRatio => {
  const { videoWidth, videoHeight } = video;

  // Finds the greatest common divisor (GCD) using the Euclidean algorithm
  const gcd = (a: number, b: number): number => b === 0 ? a : gcd(b, a % b); 🟢🟢🟢

  if (!videoWidth || !videoHeight) return AspectRatio['16:9']; 🔴🔴🔴

  const divisor = gcd(videoWidth, videoHeight);
  const aspectRatioKey = `${videoWidth / divisor}:${videoHeight / divisor}` as keyof typeof AspectRatio;
  return AspectRatio[aspectRatioKey] || AspectRatio['16:9'];

 };
```

---
### More complex:
```TS
  const handleFullscreen = useCallback(() => {
    const videoContainer = document.querySelector(`#${videoContainerId}`);
    
    if (videoContainer && videoContainer.requestFullscreen) {
      videoContainer.requestFullscreen().then(() => {
        setIsFullScreen(true);
      });
    }
  }, []);
```
## Less complex:
```TS
  const handleFullscreen = useCallback(async () => {
    const videoContainer = document.querySelector(`#${videoContainerId}`);
  
    if (!videoContainer?.requestFullscreen) return; 🔴🔴🔴
    await videoContainer.requestFullscreen();  🟣🟣🟣

    setIsFullscreen(true);
  }, []);
```

---
### More complex:
```TS
  const handleMinimise = useCallback(() => {
    if (document.fullscreenElement) {
      document.exitFullscreen().then(() => {
        setIsFullScreen(false);
      });
    }
  }, []);

```
### Less complex:
```TS
  const handleMinimise = useCallback(async () => {
    if (!document.fullscreenElement) return; 🔴🔴🔴
    await document.exitFullscreen(); 🟣🟣🟣
    setIsFullscreen(false);
  }, []);
```
