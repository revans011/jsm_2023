This is a simple two group simulation for PU data.

There are two groups, called case and control

The idea is to get some idea of how sample size, group imbalance, and
non-detection affects statistical decisions via p-values.

     now<-Sys.time()

    ###this parmlist has a very small effect size, which isn't interesting
     
    #  parmlist<-list(
    # c(rep(500,32)),             #interations; num.iter
    # c(120,60,80,90,120,60,80,90,120,60,80,90,120,60,80,90,120,60,80,90,120,60,80,90,120,60,80,90,120,60,80,90),  #cases; n.cases
    # c(60,120,80,90,60,120,80,90,60,120,80,90,60,120,80,90,60,120,80,90,60,120,80,90,60,120,80,90,60,120,80,90),  #controls unlabeled
    # c(rep(0.1,8),rep(0.05,8),rep(0.15,8),rep(0.01,8)),  #non-detection proportion
    # c(0.38,0.38,0.38,.38,0.1,0.1,0.1,0.1,0.38,0.38,0.38,0.38,0.1,0.1,0.1,0.1,0.38,0.38,0.38,.38,0.1,0.1,0.1,0.1,0.38,0.38,0.38,0.38,0.1,0.1,0.1,0.1) #treat effect
    #  )
     
    #   parmlist<-list(
    # c(rep(3000,16)),             #interations; num.iter
    # c(120,60,80,90,120,60,80,90,120,60,80,90,120,60,80,90),  #cases; n.cases
    # c(60,120,80,90,60,120,80,90,60,120,80,90,60,120,80,90),  #controls unlabeled
    # c(rep(0.1,4),rep(0.05,4),rep(0.15,4),rep(0.01,4)),  #non-detection proportion
    # c(rep(0.38,16)) #treat effect
    #  )

    #  parmlist<-list(
    # c(rep(3000,12)),             #interations; num.iter
    # rep(c(120,80,100),4),  #cases; n.cases
    # rep(c(80,120,100),4),  #controls unlabeled
    # c(rep(0.1,12)), #non-detection proportion
    # c(rep(0.4,3),rep(.1,3),rep(.9,3),rep(1.8,3)) #treat effect
    #  )
     
      
     parmlist<-list(
    c(rep(5,3)),             #interations; num.iter
    c(120,80,100),  #cases; n.cases
    c(80,120,100),  #controls unlabeled
    c(rep(0.1,3)), #non-detection proportion
    c(rep(0.4,3)) #treat effect
     )


    # ##This is to see if balance matters
    #  parmlist<-list(
    # c(rep(3000,5)),             #interations; num.iter
    # c(rep(80,5)),  #cases; n.cases
    # c(120,110,100,90,80),  #controls unlabeled
    # c(rep(0.1,5)),  #non-detection proportion
    # c(rep(0.4,5)) #treat effect
    #  )


     
    #####  #sample size matters more than direction of error
    #   parmlist<-list(
    # c(rep(500,6)),             #interations; num.iter
    # c(120,120,120,60,70,80),  #cases; n.cases
    # c(60,70,80,120,120,120),  #controls unlabeled
    # c(.05,.05,0.05,.05,.05,0.05),  #non-detection proportion
    # c(rep(.38,6)) #treat effect
    #  )
     
    foo<-pmap(parmlist,sim.fun)


    goo <- bind_rows(foo, .id = "column_label")  #unlists and binds rows


    zoo1 <- goo %>% group_by(n.cases
                            ,n.controls.unlabeled
                            ,trt.eff
                            ,prop.nondetect) %>% 
      dplyr::summarise(n.nodetec=mean(n.nondetect)
                       ,tru.minus.pu=mean(tru-pu)
                       ,pu.less.tru=mean(pu<mean(tru))
                       ,p.tru=mean(tru)
                       )

    ## `summarise()` has grouped output by 'n.cases', 'n.controls.unlabeled',
    ## 'trt.eff'. You can override using the `.groups` argument.

    knitr::kable(zoo1 %>% ungroup() %>% arrange(pu.less.tru),"simple")

<table>
<thead>
<tr class="header">
<th style="text-align: right;">n.cases</th>
<th style="text-align: right;">n.controls.unlabeled</th>
<th style="text-align: right;">trt.eff</th>
<th style="text-align: right;">prop.nondetect</th>
<th style="text-align: right;">n.nodetec</th>
<th style="text-align: right;">tru.minus.pu</th>
<th style="text-align: right;">pu.less.tru</th>
<th style="text-align: right;">p.tru</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: right;">80</td>
<td style="text-align: right;">120</td>
<td style="text-align: right;">0.4</td>
<td style="text-align: right;">0.1</td>
<td style="text-align: right;">12</td>
<td style="text-align: right;">-0.0579705</td>
<td style="text-align: right;">0.6</td>
<td style="text-align: right;">0.0421281</td>
</tr>
<tr class="even">
<td style="text-align: right;">120</td>
<td style="text-align: right;">80</td>
<td style="text-align: right;">0.4</td>
<td style="text-align: right;">0.1</td>
<td style="text-align: right;">8</td>
<td style="text-align: right;">-0.0100556</td>
<td style="text-align: right;">0.6</td>
<td style="text-align: right;">0.0760706</td>
</tr>
<tr class="odd">
<td style="text-align: right;">100</td>
<td style="text-align: right;">100</td>
<td style="text-align: right;">0.4</td>
<td style="text-align: right;">0.1</td>
<td style="text-align: right;">10</td>
<td style="text-align: right;">-0.0152300</td>
<td style="text-align: right;">0.8</td>
<td style="text-align: right;">0.0063540</td>
</tr>
</tbody>
</table>

    # %>% 
    #   kable(caption = "pu < tu sorting") %>% kable_styling(full_width = FALSE) %>% kable_classic()



    oddsratio_to_d(2,log=FALSE) #this coverts OR to cohens so that I make this like SNPs data

    ## [1] 0.3821521

    d_to_oddsratio(.1)

    ## [1] 1.198871

    oddsratio_to_d(1.2,log=FALSE)

    ## [1] 0.1005191

    print(difftime(Sys.time(),now,units="mins"))

    ## Time difference of 0.01337302 mins
