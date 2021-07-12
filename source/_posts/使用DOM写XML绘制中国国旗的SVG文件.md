---
title: Java学习:使用DOM写XML -- 绘制中国国旗的SVG文件
date: 2020-12-16 18:01:27
cover: https://raw.githubusercontent.com/PureKitS/hexo_pictures_source/main/FlagPRC.png
tags: 
- Java
- SVG
- XML
categories: Java
---





> 利用 ``Flag.java``文件绘制出一个``SVG``格式的中华人民共和国国旗。``SVG``文件参考了维基百科上的中国国旗的``SVG``文件
>
> [维基百科中华人民共和国国旗]([中华人民共和国国旗 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.wikipedia.org/wiki/中华人民共和国国旗#/media/File:Flag_of_the_People's_Republic_of_China.svg))
>
> 源码已push至GitHub [FlagPRC](https://github.com/Purekits/FlagPRC)

<!-- more -->

#### Java Code

````java
package io.pure.flagprc;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;

import javax.xml.parsers.DocumentBuilder;
import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.ParserConfigurationException;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerConfigurationException;
import javax.xml.transform.TransformerException;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.TransformerFactoryConfigurationError;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;

import org.w3c.dom.Document;
import org.w3c.dom.Element;

/**
 * 使用DOM绘制中国国旗的SVG文件
 * @author PureK1t_SVG
 * @date 2020年12月11日
 * @time PM17:20
 * @remark
 *
 */
class FlagPRC {

    /**
     * 使用DOM绘制中国国旗的SVG文件
     * @param args
     */
    public static void main(String[] args) {

        try {
            DocumentBuilderFactory factory = DocumentBuilderFactory.newInstance();
            factory.setNamespaceAware(true);
            DocumentBuilder builder = factory.newDocumentBuilder();
            //生成SVG
            Document doc = builder.newDocument();
            String namespace = "http://www.w3.org/2000/svg";
            Element elementSvg = doc.createElementNS(namespace, "svg");
            elementSvg.setAttribute("xmlns:xlink", "http://www.w3.org/1999/xlink");
            elementSvg.setAttribute("width", "900");
            elementSvg.setAttribute("height", "600");
            elementSvg.setAttribute("viewBox", "0 0 30 20");
            doc.appendChild(elementSvg);
            Element elementDef = doc.createElement("defs");
            elementSvg.appendChild(elementDef);
            Element elementPath = doc.createElement("path");
            elementPath.setAttribute("id", "s");
            elementPath.setAttribute("d",
                    "M0,-1 0.587785,0.809017 -0.951057,-0.309017H0.951057L-0.587785,0.809017z");
            elementPath.setAttribute("fill", "#ffde00");
            elementDef.appendChild(elementPath);
            Element elementRect = doc.createElement("rect");
            elementRect.setAttribute("width", "30");
            elementRect.setAttribute("height", "20");
            elementRect.setAttribute("fill", "#de2910");
            elementSvg.appendChild(elementRect);
            Element elementUse1 = doc.createElement("use");
            elementUse1.setAttribute("xlink:href", "#s");
            elementUse1.setAttribute("transform", "translate(5,5) scale(3)");
            elementSvg.appendChild(elementUse1);
            Element elementUse2 = doc.createElement("use");
            elementUse2.setAttribute("xlink:href", "#s");
            elementUse2.setAttribute("transform", "translate(10,2) rotate(23.036243)");
            elementSvg.appendChild(elementUse2);
            Element elementUse3 = doc.createElement("use");
            elementUse3.setAttribute("xlink:href", "#s");
            elementUse3.setAttribute("transform", "translate(12,4) rotate(45.869898)");
            elementSvg.appendChild(elementUse3);
            Element elementUse4 = doc.createElement("use");
            elementUse4.setAttribute("xlink:href", "#s");
            elementUse4.setAttribute("transform", "translate(12,7) rotate(69.945396)");
            elementSvg.appendChild(elementUse4);
            Element elementUse5 = doc.createElement("use");
            elementUse5.setAttribute("xlink:href", "#s");
            elementUse5.setAttribute("transform", "translate(10,9) rotate(20.659808)");
            elementSvg.appendChild(elementUse5);
            //输出到文件
            File file = new File("C:\\Users\\Purek\\Desktop\\FlagPRC.svg");
            Transformer t = TransformerFactory.newInstance().newTransformer();
            t.transform(new DOMSource(doc), new StreamResult(new FileOutputStream(file)));
        } catch (ParserConfigurationException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (TransformerConfigurationException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (TransformerFactoryConfigurationError e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (FileNotFoundException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        } catch (TransformerException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
    }
}
````

> 运行此代码之前要修改 ``84`` 行的文件目录才可以可在桌面上生成一个 ``FlagPRC.svg`` 文件 此文件可以进行使用 如果想进一步编辑此文件 可以对此文件的``XML``代码进行格式化格式方法有很多 我使用的是 在线格式化工具 [菜鸟xml在线格式化]([XML 在线格式化 | 菜鸟工具 (runoob.com)](https://c.runoob.com/front-end/710))

