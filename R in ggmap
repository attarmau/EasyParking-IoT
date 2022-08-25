library("magrittr")
library("dplyr")
library("curl")
library("stringr")
library(jsonlite)
library(ggplot2)
install.packages("googleway")
library(googleway)

#畫出地圖範圍的套件
library(ggmap)
library(mapproj)

＃如果無法import ggmap，嘗試下列五行程式碼：
if(!requireNamespace("devtools")) install.packages("devtools")
devtools::install_github("dkahle/ggmap", ref = "tidyup", force = TRUE)
library(ggmap)
register_google(key="your api key”)
devtools::install_github("dkahle/ggmap", force = TRUE)

#讀檔
taxi_on <- data.frame(lat=double(),lng=double())

#請至https://developers.google.com/maps/?hl=zh-tw 取得api key
key <- "your api key"
for (i in 1:length(taxi_on)) {
  geo_result <- google_geocode(address = taxi_on[i], key = key)
  taxi_on_map<-rbind(taxi_on_map,geo_result$results$geometry$location)
  #由於google api每秒鐘有資料讀取限制，因此這邊設定迴圈0.01秒執行一次
  Sys.sleep(0.01)
}

#畫出地圖範圍
#參考：https://blog.gtwang.org/r/r-ggmap-package-spatial-data-visualization/
map <- get_map(location = c(lon = 121.05, lat = 25.05),
               zoom = 11, language = "zh-TW")
ggmap(map)+
  geom_point(aes(x = lng, y = lat), size = 1, col="red",data = area_kao, alpha = 0.6)+
  geom_density2d(data = area_kao, aes(x = lng, y=lat), size = 0.3, geom = "polygon")
  
#error參考：https://mlog.club/article/5150943
