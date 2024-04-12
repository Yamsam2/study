# SQLite DB생성 페이지 예제        
   
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
        NaverMapSdk.getInstance(this).setClient(new NaverMapSdk.NaverCloudPlatformClient("xy"));
        MapView mapView_auto = (MapView) findViewById(R.id.mapView_auto);
        locationSource = new FusedLocationSource(this, PERMISSION_REQUEST_CODE);
        mapView_auto.getMapAsync(this);
```
 
  
curcor에 테이블 넣기  
```java
sqlDB = resultDB.getReadableDatabase();  
Cursor cursor;  
cursor = sqlDB.rawQuery("SELECT * FROM log_library;", null);   
```
  
Curosr 이동방법  
  
 
cursor.moveToFirst() : Cursor를 제일 첫번째 행(Row)으로 이동 시킨다.  
cursor.moveToNext() : Cursor를 다음 행(Row)으로 이동 시킨다.  
cursor.moveToPrevious() : Cursor를 이전 행(Row)으로 이동 시킨다.  
cursor.moveToPosition(position) : Cursor를 해당 Position 행(Row)으로 이동 시킨다.  
cursor.moveToLast() : Cursor를 마지막 행(Row)으로 이동 시킨다.  


Cursor 변수에 담기  
원하는 row에 Cursor위치시키고,  
변수 = cursor.getString(index값)   



