library(RSelenium)
remDr<-remoteDriver(remoteServerAddr = "localhost", port=4445, browserName="chrome")

remDr$open();
site<- paste("http://www.yes24.com/24/goods/40936880")
remDr$navigate(site)
webElem<- remDr$findElement("css", "body")

fullContentLinkCSS<- "//*[@id=\"yDetailTabNavWrap\"]/div/div/ul/li[2]/a"
fullContentLink<-remDr$findElements(using='xpath',  fullContentLinkCSS)
sapply(fullContentLink,function(x){x$clickElement()})
Sys.sleep(1)

repl_v = NULL

repeat{
  for(PA in 3:12){ 
    for(i in 2:6){
      path<-paste0("//*[@id=\"infoset_reviewContentList\"]/div[",i,"]/div[5]/a");
      full<-remDr$findElements(using='xpath', value=path)
      if(length(full)==0){
        break
      }else{
        sapply(full,function(x){x$clickElement()})
        Sys.sleep(2)
      }
    }  
    for(i in 2:6){
      fullContentCSS<- paste0("//*[@id=\"infoset_reviewContentList\"]/div[",i,"]/div[3]/div[2]")
      fullContent<-remDr$findElements(using='xpath', fullContentCSS)
      print(fullContent)
      repl<-sapply(fullContent,function(x){x$getElementText()})
      if(length(repl)==0){
        break
      }else{
        repl<-gsub("\n\n","",repl)   
        repl<-gsub("\n","",repl)
        
        print(repl)
        repl_v<- c(repl_v, unlist(repl))
        Sys.sleep(1)
      }
    }
    if(PA!=12){
      fullContentLinkCSS<- paste0("//*[@id=\"yDetailTabNavWrap\"]/div/div/ul/li[2]/a")
      fullContentLink<-remDr$findElements(using='xpath',  fullContentLinkCSS)
      sapply(fullContentLink,function(x){x$clickElement()})
      Sys.sleep(1)
      
      fullContentLinkCSS<- paste0("//*[@id=\"infoset_reviewContentList\"]/div[1]/div[1]/div/a[",PA,"]")
      fullContentLink<-remDr$findElements(using='xpath',  fullContentLinkCSS)
      sapply(fullContentLink,function(x){x$clickElement()})
      Sys.sleep(2)
    }else{
      
      fullContentLinkCSS<- paste0("//*[@id=\"yDetailTabNavWrap\"]/div/div/ul/li[2]/a")
      fullContentLink<-remDr$findElements(using='xpath',  fullContentLinkCSS)
      sapply(fullContentLink,function(x){x$clickElement()})
      Sys.sleep(1)
      
      css1<- paste0("#infoset_reviewContentList > div.review_sort.sortTop > div.review_sortLft > div > a.bgYUI.next")
      link<-remDr$findElements(using='css',  css1)
      sapply(link,function(x){x$clickElement()})
      Sys.sleep(2)
      
      fullContentCSS<- "//*[@id=\"infoset_reviewContentList\"]/div[2]/div[3]/div[2]"
      fullContent<-remDr$findElements(using='xpath', fullContentCSS)
      repl<-sapply(fullContent,function(x){x$getElementText()})
      Sys.sleep(1)
      
      repl<-unlist(repl)
    }
  }
}

write(repl_v, "yes24.txt")