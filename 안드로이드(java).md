  ## 안드로이드s 

clearAnimation*  
애니메이션 XML에 fillAfter="true" 가 되 있으면 애니메이션이 끝나더라도 마지막 프레임이 계속 남아있어  
visibility = "gone", "invisible" 등의 작동이 안됨  
false로 바꾸거나 clearAnimation()을 호출하자    
   
     
엑티비티 모두 종료가 필요할 때(로그아웃 등)*     
ActivityCompat.finishAffinity(this);      
    
          
안드로이드 고유 기기번호(ANDROID_ID) : 디바이스 초기화시 번호가 변경됨*               
String android_id = Settings.Secure.getString(this.getContentResolver(),Settings.Secure.ANDROID_ID);              
     
    
   
  /*모든파일 관리 허용       
  requestPermission에는 모든파일이 권한요청이 포함되어있지않기 때문에 Intent를 이용해서 요청해야됨     
  startActivityForResult는 deprecated 되었기때문에 이제는Uri주소를 이용해서 기기 디바이스 화면으로 넘겨야함    
  */     
  if (Environment.isExternalStorageManager()){   
  }else{    
   Intent intent = new Intent();   
   intent.setAction(Settings.ACTION_MANAGE_APP_ALL_FILES_ACCESS_PERMISSION);  
   Uri uri = Uri.fromParts("package", this.getPackageName(), null);   
   intent.setData(uri);   
    startActivity(intent);   
  }  
     

     
 * 테이블 레이아웃 동적으로 row 추가 하기 (vertical)*  
 ```java
chartRowArr.clear(); 

chartRowArr.add(String.valueOf(nodeSaveArr.size()));
chartRowArr.add(nodeSaveArr.get(nodeSaveArr.size()-1));
chartRowArr.add("");
int min, sec; //분초로 변경
min = nodeSaveArrTimer.get(nodeSaveArrTimer.size()-1) / 60;
sec = nodeSaveArrTimer.get(nodeSaveArrTimer.size()-1) % 60;
min = min % 60;
chartRowArr.add(min+":"+sec);

tableRow = new TableRow(this); //새 row 생성
for(int i=0; i<4; i++){ //TextView에 각 속성의 값들 추가
    TextView textView = new TextView(getApplicationContext());
    textView.setText(chartRowArr.get(i));
    textView.setGravity(Gravity.CENTER);
    textView.setTypeface(null, Typeface.BOLD);
    textView.setTextSize(19);
    tableRow.addView(textView); //row에 textView 추가
}
//생성한 row를 테이블에 추가
tableLayout.addView(tableRow, new TableLayout.LayoutParams(ViewGroup.LayoutParams.MATCH_PARENT, ViewGroup.LayoutParams.WRAP_CONTENT));  
```

        
* 화면 바깥 터치 시 소프트키보드 내리기
```java
@Override
public boolean dispatchTouchEvent(MotionEvent ev) {
    View view = getCurrentFocus();
    if (view != null && (ev.getAction() == MotionEvent.ACTION_UP || ev.getAction() == MotionEvent.ACTION_MOVE) && view instanceof EditText && !view.getClass().getName().startsWith("android.webkit.")) {
        int scrcoords[] = new int[2];
        view.getLocationOnScreen(scrcoords);
        float x = ev.getRawX() + view.getLeft() - scrcoords[0];
        float y = ev.getRawY() + view.getTop() - scrcoords[1];
        if (x < view.getLeft() || x > view.getRight() || y < view.getTop() || y > view.getBottom())
            ((InputMethodManager) this.getSystemService(Context.INPUT_METHOD_SERVICE)).hideSoftInputFromWindow((this.getWindow().getDecorView().getApplicationWindowToken()), 0);
    }
    return super.dispatchTouchEvent(ev);
}
```


* 카운트다운 타이머(java) - 일정 시간 루틴으로 코드를 반복해야 할 때
```java
CountDownTimer = timeCircle;
timerCircle = new CountDownTimer(90000000, 1000) { //반복 할 총 시간, 반복 주기(1000은 1초)
  @Override
  public void onTick(long l) {
    //반복할 코드
  }
    @Override
    public void onFinish() {
      //끝났을 때 실행 할 코드
    }
}.start();
```


* 핸들러로 딜레이 주기 - 코드를 일정 시간 후 실행 해야 할 때
  
```java
Handler handlerMakeCircle = new Handler();
handlerMakeCircle.postDelayed(new Runnable() {
    public void run() {
        //실행 할 코드
    }
}, 1500); //1.5초후

```

 
