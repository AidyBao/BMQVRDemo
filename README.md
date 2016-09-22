# BMQVRDemo
一个简单的VR,暂时只实现了图片旋转,图片点击事件后续再补上


1.导入AVFoundation.framework
CoreGraphics.framwork
Foundation.framework
CoreLocation.framework


2.监听磁场
    self.locationManager = [[CLLocationManager alloc]init];
    self.locationManager.delegate = self;
    [self.locationManager requestWhenInUseAuthorization];
    [self.locationManager startUpdatingHeading];
  
3.开启陀螺仪
代码太长，看Demo

4.开启摄像头
    _device = [AVCaptureDevice defaultDeviceWithMediaType:AVMediaTypeVideo];
    // Input
    _input = [AVCaptureDeviceInput deviceInputWithDevice:self.device error:nil];
    // Output
    _output = [[AVCaptureMetadataOutput alloc]init];
    [_output setMetadataObjectsDelegate:self queue:dispatch_get_main_queue()];
    // Session
    _session = [[AVCaptureSession alloc]init];
    
    [_session setSessionPreset:AVCaptureSessionPresetMedium];
    
    if ([_session canAddInput:self.input])
    {
        [_session addInput:self.input];
    }
    if ([_session canAddOutput:self.output])
    {
        [_session addOutput:self.output];
    }
    // 条码类型 AVMetadataObjectTypeQRCode
    _output.metadataObjectTypes =@[AVMetadataObjectTypeQRCode];
    
    // Preview
    _preview =[AVCaptureVideoPreviewLayer layerWithSession:_session];
    _preview.videoGravity = AVLayerVideoGravityResizeAspectFill;
    _preview.frame =CGRectMake(0,0,APP_FRAME_WIDTH,APP_FRAME_HEIGHT);
    [_session startRunning];
