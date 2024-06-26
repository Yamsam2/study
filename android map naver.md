# 네이버 맵 생성 페이지 예제       


## onCreate 안에   
```java
@Override
    public void onMapReady(@NonNull NaverMap naverMap) {
        mNaverMap = naverMap;
        mNaverMap.setLocationSource(locationSource);
        ActivityCompat.requestPermissions(this, PERMISSIONS, PERMISSION_REQUEST_CODE);
        UiSettings uiSettings = mNaverMap.getUiSettings();
 
        uiSettings.setScaleBarEnabled(false);

        LocationButtonView locationButtonView = findViewById(R.id.location);
        locationButtonView.setMap(mNaverMap);
        naverMap.setFpsLimit(60);

        naverMap.setMinZoom(7);
        naverMap.setMaxZoom(17);
//        naverMap.getUiSettings().setLocationButtonEnabled(false);
        naverMap.getUiSettings().setLogoGravity(Gravity.RIGHT | Gravity.BOTTOM);
        naverMap.getUiSettings().setLogoMargin(20, 20, 20, 20);

        //네이버 맵 오버레이
        LocationOverlay locationOverlay = mNaverMap.getLocationOverlay();
        locationOverlay.setIcon(OverlayImage.fromResource(R.drawable.car_icon_human));

        locationOverlay.setBearing(100);

        naverMap.getLocationOverlay().setCircleRadius(150);
        naverMap.getLocationOverlay().setCircleColor(Color.argb(22, 102, 102, 255));

        try {
            insertMarker();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
    
``` 
    
## 네이버맵 적용
```java
        //네이버맵 onCreate에 적용, 네이버 location 적용
        NaverMapSdk.getInstance(this).setClient(new NaverMapSdk.NaverCloudPlatformClient("클라이언트아이디입력"));
        MapView mapView_auto = (MapView) findViewById(R.id.mapView_auto);
        locationSource = new FusedLocationSource(this, PERMISSION_REQUEST_CODE);
        mapView_auto.getMapAsync(this);
```

## 폴리곤 생성
```java
    //뉴뉴
    public void polygonSquare() {

        Marker marker = new Marker();
        marker.setPosition(new LatLng(35.145263, 129.066096));
        marker.setMap(mNaverMap);


        //폴리곤 생성 테스트
        PolygonOverlay polygon = new PolygonOverlay();
        polygon.setCoords(Arrays.asList(
                new LatLng(35.145263, 129.066096),
                new LatLng(35.144960, 129.065993),
                new LatLng(35.144986, 129.067507),
                new LatLng(35.145469, 129.067247)
        ));
        //16진수 컬러 직접 입력 시
        //polygon.setColor(Color.parseColor("#80847223"));
        //자바 기본색상
        polygon.setColor(Color.GREEN);
        polygon.setMap(mNaverMap);

        PolylineOverlay polyline = new PolylineOverlay();
        polyline.setCoords(Arrays.asList(
                new LatLng(35.145263, 129.066096),
                new LatLng(35.145469, 129.067247),
                new LatLng(35.144960, 129.065993),
                new LatLng(35.144986, 129.067507)
        ));
        polyline.setWidth(10);
        polyline.setMap(mNaverMap);
    }

//함수 실행은 onMapReady 안쪽에

```

## 중앙 점(좌표)을 이용하여 사각형 생성


```java
    double latChange = metersToLatitude(radiusInMeters);
    double lngChange = metersToLongitude(centerPoint.latitude, radiusInMeters);
    
    // 정사각형의 네 꼭짓점 계산
    LatLng[] squarePoints = new LatLng[4];
    squarePoints[0] = new LatLng(centerPoint.latitude + latChange, centerPoint.longitude - lngChange);
    squarePoints[1] = new LatLng(centerPoint.latitude + latChange, centerPoint.longitude + lngChange);
    squarePoints[2] = new LatLng(centerPoint.latitude - latChange, centerPoint.longitude + lngChange);
    squarePoints[3] = new LatLng(centerPoint.latitude - latChange, centerPoint.longitude - lngChange);


    private double metersToLatitude(double meters) {
        return meters / 111111.0;
    }
    private double metersToLongitude(double latitude, double meters) {
        double latRadians = Math.toRadians(latitude);
        return meters / (111111.0 * Math.cos(latRadians));
    }
```




