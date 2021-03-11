### day 13: Folium

### `folium으로 동적 지도를 구현하라. 위치 한 곳을 정해서 그 위치를 중심으로 지도를 그리고 마커를 출력한다. 마커위에 마우스를 올리면 적당한 메시지로 툴팁을 출력하고, 마커를 클릭하면 적당한 메시지가 윈도우로 출력되는 기능까지 구현한다.`

``` python
import folium

home = folium.Map(location=[37.4802,126.9264], zoom_start=15)

tooltip = '우리 댕댕이가 기다리고있는 집입니다 빨리 가고싶어요 흐그흐그흐흑'
icon = folium.Icon(color='black', icon='cloud') # 검정색 구름 마커
folium.Marker([37.4802,126.9264], popup='<div style="width:400px"><h4><b>멍멍멍ㅁ! 관악구 멍멍이!</b></h4></div>', tooltip=tooltip, icon=icon).add_to(home)

display(home)
home.save('output/hw4.html')
```

