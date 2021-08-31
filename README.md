# Neuroscience-KI

## This README.md file is used for bioinformatic learning

### Reference link: https://www.jianshu.com/p/b719f3f306a1

# 如何批量计算相关性

1.只计算相关性，不考虑显著性检验：

```R
library(corrr)
library(dplyr)
data(mtcars)
mtcars%>%correlate()%>%rearrange()%>%stretch()
```

2.计算两种结果：

```R
library(dplyr)
library(purrr)
library(broom)
library(tidyr)
data(mtcars)
pairs_names<-t(combn(names(mtcars),2))%>%
as_tibble()%>%
setNames(c("x","y"))

pairs_names%>%
mutate(r.test=map2(x,y,~cor.test(mtcars[[.x]],
mtcars[[.y]])),r.test=map(r.test,tidy))%>%
unnest(r.test)
```

