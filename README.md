GPTCelltypeSXY: 
====
基于GPT4模型对scRNA分群进行自动注释(国内网络可用)

# 单细胞注释工具
GPTcelltype(发表在Nature Method)

**基于GPT4模型对scRNA分群进行自动注释(国内网络可用)**

**安装音云API专用GPT注释的两个包**

```
remotes::install_github("xiehs211/apiSXY")
remotes::install_github("xiehs211/GPTCelltypeSXY")
```

# 设置GPT令牌

```
usethis::edit_r_environ()
```

增加内容

```
OPENAI_API_KEY=sk-fxxxxxxxxxxxx
OPENAI_API_URL=https://xxxxxxxxxxx/v1
```

分别是令牌和对应的调用站点url。保存后，再重启Rstudio
```
Sys.getenv("OPENAI_API_KEY")
Sys.getenv("OPENAI_API_URL")
```
就可以获得当前的变量，刚好校验是否设置成功。
# 导入安装的R包自动注释
```
library(apiSXY)
library(GPTCelltypeSXY)
```
markers是一个list, 也可以是Seurat FindAllMarkers()出来的data.frame
```
markers <- list("C0" = c("Ager", "Hopx", "Pdpn")) # 这里的例子为了方便是一个自定义list
# model表示使用哪个大语言模型(可以是gpt4, gpt4o, gpt-4-turbo)
# tissuename表示你需要注释的组织/器官等，比如肺癌单细胞测序(scRNA data of lung cancer)、癌症类器官(organoids of cancer)等
res <- gptcelltype(markers, tissuename = "lung", model = 'gpt-4o') # 这里基于上述给定的markers对肺(lung)进行注释
res
# C0 
# "Alveolar Type 1 Cells" 
```
**示例过程(注意2处红线指出的地方yinyunapi，代表成功调用了函数)**

![image-20251010105755786](https://book.sxycloud.com/_images/image-20251010105755786-1760065076967-1.png)
