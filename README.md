if(app.activeDocument.name.search(/S\d+\-\d+.indd|S\d+\_\d+.indd/)!==-1){
app.doScript('/Volumes/spring-work/JYSK/1_Design Manual/Indesign Script/Script by Quang/file goc/Check Layer.jsx')  
}
else{
    #targetengine "session";
    var myName = myInput ();
    // rest of the script
    function myInput () {
        var myWindow = new Window ("dialog", "Name Of Page");
        var myInputGroup = myWindow.add ("group");
        var list = myInputGroup.add ("statictext", undefined, "Name:");
        var myText = myInputGroup.add ("edittext", undefined, "");
        myText.minimumSize = myText.maximumSize=[200,20]
        myText.active = true;
        var myButtonGroup = myWindow.add ("group");
        myButtonGroup.alignment = "right";
        myButtonGroup.add ("button", undefined, "OK");
        myButtonGroup.add ("button", undefined, "Cancel");

        if (myWindow.show () == 1) {
            var a = []
            for(var m=0;m<app.documents.length;m++){
                if(myText.text+".indd"==app.documents[m].name){
                    a.push(app.documents[m])
                }
            }
            if(a.length==0){
                alert("Sai Ten Page")
            }
            else{
            var doc1 = app.documents.itemByName(myText.text+".indd");
            var doc = app.activeDocument
            var b = []
            var text = []
            var insert =[]
            var imagess = []
            var cmmanus = []
            var infomanus = []
            var selectext = []
            var selectlogo = []
            var colorinsert = []
            var thongbaotext = []
            var commentmanus = []
            var compare_price = []
            var thieutext_page = []
            var colorinsertpage = []
            var thieutext_manus = []
            var logo_saving_page = []
            var new_graphic_page = []
            var logo_saving_manus = []
            var new_graphic_manus = []
            
            var name_pagenumber1 = doc1.name.substr(-7,2)
            var name_pagenumber2 = doc1.name.substr(-10,2)

            var item1=doc1.allPageItems;
            for (var x=0;x<item1.length;x++){
                if(item1[x].constructor.name=='Oval'&&item1[x].geometricBounds[3]-item1[x].geometricBounds[1]<12){
                    colorinsertpage.push(item1[x])
                }
                if(item1[x].constructor.name=='PDF'||item1[x].constructor.name=='Image'||item1[x].constructor.name=='EPS'){
                    imagess.push(item1[x].itemLink.name.match(/\d+{3,}/g))  
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&(item1[x].parentStory.appliedParagraphStyle.name=="_Promotiondescription - Black"||item1[x].parentStory.appliedParagraphStyle.name=="_Promotiondescription - White"
                ||item1[x].parentStory.appliedParagraphStyle.name=="_Promotiontext - Black"||item1[x].parentStory.appliedParagraphStyle.name=="_Promotiontext - White"||item1[x].parentStory.appliedParagraphStyle.name=="[Basic Paragraph]")&&item1[x].contents.search(/\w/g)!==-1){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                    thieutext_page.push(item1[x])   
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&item1[x].parentStory.appliedParagraphStyle.name!=="_Promotiondescription - Black"&&item1[x].parentStory.appliedParagraphStyle.name!=="_Promotiontext - Black"
                &&item1[x].appliedObjectStyle.name=="01 Short text in images"&&item1[x].paragraphs[0].pointSize<=7.5){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                    thieutext_page.push(item1[x])   
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&item1[x].parentStory.appliedParagraphStyle.name=="_Textbar"){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""))
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&item1[x].parentStory.appliedParagraphStyle.name=="NEW graphic"){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                    new_graphic_page.push(item1[x])
                }
                if(item1[x].constructor.name=='Oval'&&item1[x].itemLayer.name==="Text/Graphic"){
                    if(item1[x].allPageItems.length>0){
                        if(item1[x].allPageItems[0].constructor.name=="Rectangle"||item1[x].allPageItems[0].constructor.name=="Image"){
                            insert.push(item1[x])
                        }
                    } 
                     else{
                        if(item1[x].strokeColor.name=="Black"){
                            insert.push(item1[x])
                        }
                        else{
                            text.push(item1[x].textPaths[0].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                            thieutext_page.push(item1[x])
                        }
                    }
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&item1[x].parentStory.appliedParagraphStyle.name.slice(0,14)=="_Campaignprice"){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&(item1[x].parentStory.appliedParagraphStyle.name.slice(0,4)=="_PIF"||item1[x].appliedObjectStyle.name=="04 PIF transparent")&&item1[x].contents.search(/\w/g)!==-1){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""))
                    //b.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                }
                if(item1[x].constructor.name=='TextFrame'&&item1[x].itemLayer.name==="Text/Graphic"&&item1[x].parentStory.appliedParagraphStyle.name=="FR_Eco"&&item1[x].appliedObjectStyle.name!=="04 PIF transparent"){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                }
                if(item1[x].constructor.name=='PDF'&&item1[x].itemLayer.name==="Text/Graphic"&&item1[x].itemLink.filePath.substr(-8,8)!=='42301.ai'&&item1[x].itemLink.filePath.substr(-9,9)!=='161126.ai'&&item1[x].itemLink.filePath.search(/\d+.ai/g)!==-1&&item1[x].itemLink.name.search(/Sale/g)==-1){
                   logo_saving_page.push(item1[x].itemLink.name);
                   text.push(item1[x].itemLink.name);
                }
                if (item1[x].itemLayer.name==="Articlenum"){
                    text.push(item1[x].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                  }
            }

            for (var i =doc.pages.length-1;i>=0;i--){
                var textframe=doc.pages[i].textFrames;
                var page_manus=0;
                for (var j =0; j<textframe.length;j++){
                    if((textframe[j].itemLayer.name=="Info/Comments"||textframe[j].itemLayer.name=="Info/Comments copy 1")&&textframe[j].parentStory.contents.slice(0,4)!=='00'+name_pagenumber1&&textframe[j].parentStory.contents.slice(0,4)!=='00'+name_pagenumber2){
                        page_manus+=1;
                    }
                }
                if(page_manus==0){
                    var item=doc.pages[i].allPageItems
                    for ( var z=0;z<item.length;z++){
                        if(item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name=="Info/Comments copy 1"&&item[z].contents.search(/color insert|COLOR INSERT|color INSERT|COLOR insert|colour insert/g)!==-1){
                            colorinsert.push(item[z])
                        }
                        if((item[z].itemLayer.name==="Info/Comments copy 1"||item[z].itemLayer.name==="Info/Comments")&&item[z].contents.search(/ID|insert|logo|icon|id|Id|iD|function|Function|picture/g)!==-1){
                            var a = item[z].contents.match(/\d{5,}/g) ;
                            if(a!==null){
                                for (var q=a.length;q>=0;q--){
                                    if(a[q]!==undefined){
                                        cmmanus.push(a[q]) 
                                    }
                                }
                            }
                        }
                        if(item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name=="Info/Comments copy 1"&&item[z].contents.length>30&&item[z].contents.search(/color insert|COLOR INSERT|color INSERT|COLOR insert|colour insert|ID|insert|logo|icon|id|Id|iD|function|Function|picture/g)==-1){
                            infomanus.push(item[z].contents)
                        }

                        if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&(item[z].parentStory.appliedParagraphStyle.name=="_Promotiondescription - Black"||item[z].parentStory.appliedParagraphStyle.name=="_Promotiontext - Black"||item[z].parentStory.appliedParagraphStyle.name=="_Promotiontext - White")
                        &&item[z].contents.search(/Graphics|graphic|Scandinavian|Customer|CUSTOMER|TOP 10|Top 10|Скандинавский|Skandinavisch/g)==-1&&item[z].contents.search(/\w/g)!==-1&&item[z].fillColor.name==="None"&&item[z].contents.search(/www.spring-production.com/g)==-1){
                           if(item[z].contents.search(/Vertical side text|Vertical Side Text|VERTICAL SIDE TEXT|vertical side text/g)!==-1){
                                text.push(item[z].paragraphs[1].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                                thieutext_manus.push(item[z].contents)
                                b.push(item[z].paragraphs[1].contents.replace(/\n|\r|\s|\uFEFF/g, ""))
                            }
                            else{
                               text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                               thieutext_manus.push(item[z].contents);
                           }
                        }
                        if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&item[z].fillColor.name==="C=15 M=100 Y=100 K=0"){
                            // item[z].parentStory.appliedParagraphStyle=doc.paragraphStyles.itemByName("_Promotiondescription - White");
                            item[z].contents = item[z].contents.toUpperCase()
                            item[z].fit(FitOptions.frameToContent)
                            text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF|\(LINEBREAK\)|\(LINE BREAK\)/g, ""));
                            thieutext_manus.push(item[z]);
                        }
                        if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&(item[z].parentStory.appliedParagraphStyle.name=="_Promotiondescription - Black"||item[z].parentStory.appliedParagraphStyle.name=="_Promotiontext - Black")
                        &&item[z].contents.search(/www.spring-production.com/g)!==-1){
                           text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                           thieutext_manus.push(item[z])
                        }
                        if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&item[z].parentStory.appliedParagraphStyle.name=="_Textbar"){
                           text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                        }
                        if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&item[z].parentStory.appliedParagraphStyle.name=="NEW graphic"){
                           text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                           new_graphic_manus.push(item[z])
                        }
                        if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&item[z].parentStory.appliedParagraphStyle.name.slice(0,14)=="_Campaignprice"){
                           text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                        }
                        if (item[z].itemLayer.name==="Articlenum"&&item[z].contents.search(/\d+/g)!==-1){
                           text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                        }
                         if (item[z].constructor.name=='TextFrame'&&item[z].itemLayer.name==="Text/Graphic"&&(item[z].parentStory.appliedParagraphStyle.name.slice(0,4)=="_PIF"||item[z].parentStory.appliedParagraphStyle.name=="FR_Eco")&&item[z].contents.search(/\w/g)!==-1){
                           text.push(item[z].contents.replace(/\n|\r|\s|\uFEFF/g, ""));
                        }
                        if(item[z].constructor.name=='PDF'&&item[z].itemLink.filePath.substr(-8,8)!=='42301.ai'&&item[z].itemLink.filePath.substr(-9,9)!=='161126.ai'){
                           logo_saving_manus.push(item[z].itemLink.name);
                           text.push(item[z].itemLink.name);   
                        }
                    }
                }
            }

            function count_duplicate_price(text){
            var counts = {}

            for(var t =0; t < text.length; t++){ 
                if (counts[text[t]]){
                    counts[text[t]] += 1
                } 
                else {
                    counts[text[t]] = 1
                }
            }  
                for (var prop in counts){
                    if (counts[prop]%2 !== 0){
                        compare_price.push(prop) 
                    }
                }
            }
            count_duplicate_price(text)

            Array.prototype.tontai=function(search){
                for(var k=0;k<this.length;k++)
                    if(this[k]==search) return this[k];
                    return false;
                    }

            for (var i =doc.pages.length-1;i>=0;i--){
                var textframe=doc.pages[i].textFrames;
                var page_manus=0;
                for (var j =0; j<textframe.length;j++){
                    if((textframe[j].itemLayer.name=="Info/Comments copy 1"||textframe[j].itemLayer.name=="Info/Comments")&&textframe[j].parentStory.contents.slice(0,4)!=='00'+name_pagenumber1&&textframe[j].parentStory.contents.slice(0,4)!=='00'+name_pagenumber2){
                        page_manus+=1;
                        }
                    }
                if(page_manus==0){
                    var item2=doc.pages[i].allPageItems;
                    for(var k=0;k<compare_price.length;k++){
                        for (var x=0;x<item2.length;x++){
                            if(item2[x].constructor.name=='TextFrame'){
                                if(item2[x].contents.replace(/\n|\r|\s|\uFEFF/g, "")==compare_price[k]){
                                    selectext.push(item2[x]);
                                    thongbaotext.push(item2[x]);
                                }
                                if(item2[x].contents.search(/Vertical side text|Vertical Side Text|VERTICAL SIDE TEXT|vertical side text/g,)!==-1){
                                    if(item2[x].paragraphs[1].contents.replace(/\n|\r|\s|\uFEFF/g, "")==compare_price[k]){
                                        selectext.push(item2[x]);
                                        thongbaotext.push(item2[x]);
                                    }
                                }
                            }
                            if(item2[x].constructor.name=='PDF'){
                                if(selectlogo.tontai(item2[x].itemLink.name)){}
                                else{
                                    if(item2[x].itemLink.name==compare_price[k]){
                                        selectlogo.push(item2[x].itemLink.name);
                                        selectext.push(item2[x]);
                                    }
                                }
                            } 
                        }
                    }
                    for (var x=0;x<item2.length;x++){
                        if(item2[x].itemLayer.name=="Info/Comments copy 1"){ 
                            for(var g=0;g<cmmanus.length;g++){
                                if(imagess.tontai(cmmanus[g])){}
                                else{
                                    if(item2[x].contents.search(cmmanus[g])!==-1){
                                        selectext.push(item2[x]);
                                        commentmanus.push(item2[x]);
                                    }
                                }
                            } 
                        }
                    }
                }
            }
            if(insert.length!==0){
                alert("Có insert sai layer hoặc group sai layer")
            }
            else{
                if (logo_saving_manus.length-logo_saving_page.length<0){var bc =0}
                if (logo_saving_page.length-logo_saving_manus.length<0){var cb =0}
                if (logo_saving_manus.length-logo_saving_page.length==0&&logo_saving_page.length-logo_saving_manus.length==0){
                    var bc =logo_saving_manus.length-logo_saving_page.length
                    var cb =logo_saving_page.length-logo_saving_manus.length}
                if (logo_saving_manus.length-logo_saving_page.length>0){var bc =logo_saving_manus.length-logo_saving_page.length}
                if (logo_saving_page.length-logo_saving_manus.length>0){var cb =logo_saving_page.length-logo_saving_manus.length}

                if(selectext.length == 0&&logo_saving_manus.length-logo_saving_page.length==0&&logo_saving_page.length-logo_saving_manus.length==0&&thieutext_manus.length-thieutext_page.length<=0
                &&new_graphic_manus.length-new_graphic_page.length==0&&colorinsert.length-colorinsertpage.length==0){
                    alert("perfect")
                    if(infomanus.length!==0){
                        alert("Nho Check Lai Comments")
                    }
                    var w = new Window ("dialog","Result");
                    w.add ("statictext", undefined, "Chuẩn Bị Check Spread, Bạn Có Muốn Tiếp Tục Không");
                    var mybutton = w.add("group")
                    mybutton.alignment = "right";
                    mybutton.add ("button", undefined, "Ok");
                    mybutton.add ("button", undefined, "Cancel");
                    if(w.show()==1){
                        app.activeDocument=doc1
                        app.doScript('/Volumes/spring-work/JYSK/1_Design Manual/Indesign Script/Script by Quang/file goc/Check Layer.jsx')
                    }
                    
                }
                else{
                     var w=new Window('palette','Check Info')
                     var thieu=bc+' Thiếu Logo hoặc Saving'
                     var du=cb+' Dư Logo hoặc Saving'
                     var loisai=selectext.length+' Lỗi Sai:'
                     var saitext=thongbaotext.length+' Sai Text Hoặc Giá'
                     var thieutext=thieutext_manus.length-thieutext_page.length+' Thiếu Text'
                     var newbar=new_graphic_manus.length-new_graphic_page.length+' Thiếu Newbar'

                    if(thongbaotext.length!==0){
                        var panel1=w.add('statictext',undefined,saitext)
                    }
                    if(colorinsertpage.length<colorinsert.length){
                        var panel2=w.add('statictext',undefined,colorinsert.length-colorinsertpage.length+' Color Insert Thiếu')
                    }
                    if(bc!==0){
                        var panel3=w.add('statictext',undefined,thieu)
                    }
                    if(cb!==0){
                        var panel4=w.add('statictext',undefined,du)
                    }
                    if(thieutext>1){
                        var panel5=w.add('statictext',undefined,thieutext)
                    }
                    if(new_graphic_manus.length-new_graphic_page.length>1){
                        var panel6=w.add('statictext',undefined,newbar)
                    }
                    if(commentmanus.length!==0){
                        var panel7=w.add('statictext',undefined,commentmanus.length+' Comment Chưa Làm')
                    }
                    if(panel1==undefined&&panel2==undefined&&panel3==undefined&&panel4==undefined&&panel5==undefined&&panel6==undefined&&panel7==undefined&&selectext.length!==0){
                        panel8=w.add('statictext',undefined,'ID Khac Nhau')
                    }
                    if(selectext.length>1){
                        panel8=w.add('statictext',undefined,'Bấm next để chọn Lỗi Sai')
                    }


                    w.buttons = w.add ('group {alignment: "right"}');
                    var next=w.buttons.add ('button {text: "Next"}');
                    var can=w.buttons.add ('button {text: "Cancel"}');

                    var y=0
                    run()
                    function run(){
                        if(y==selectext.length){
                            if(selectext.length!==0){
                            alert("Done")
                            w.close()
                            app.activeWindow.zoomPercentage=100
                            if(infomanus.length!==0){
                                alert("Nho Check Lai Comments")
                            }
                            var table = new Window ("dialog","Result");
                            table.add ("statictext", undefined, "Chuẩn Bị Check Spread, Bạn Có Muốn Tiếp Tục Không");
                            var mybutton = table.add("group")
                            mybutton.alignment = "right";
                            mybutton.add ("button", undefined, "OK");
                            mybutton.add ("button", undefined, "Cancel");
                            if(table.show()==1){
                                app.activeDocument=doc1
                                app.doScript('/Volumes/spring-work/JYSK/1_Design Manual/Indesign Script/Script by Quang/file goc/Check Layer.jsx')
                            }
                            }
                        }
                        else{
                            selectext[y].select()
                            app.activeWindow.zoomPercentage=100;
                        }
                    }
                    next.onClick=function(){
                        if(selectext.length==0){
                            alert("Done")
                            w.close()
                            var table = new Window ("dialog","Result");
                            table.add ("statictext", undefined, "Chuẩn Bị Check Spread, Bạn Có Muốn Tiếp Tục Không");
                            var mybutton = table.add("group")
                            mybutton.alignment = "right";
                            mybutton.add ("button", undefined, "OK");
                            mybutton.add ("button", undefined, "Cancel");
                            if(table.show()==1){
                                app.activeDocument=doc1
                                app.doScript('/Volumes/spring-work/JYSK/1_Design Manual/Indesign Script/Script by Quang/file goc/Check Layer.jsx')
                            }
                        }
                        else{
                            y=y+1
                            return run()
                        }
                        
                    }
                    can.onClick=function(){
                        w.close()
                    }
                    w.show() 
                    }
                }
            }  
        }
    }
}



