# myinf
meu repositorio
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package br.com.infsolution.infclin;


import com.itextpdf.text.BaseColor;
import com.itextpdf.text.Document;
import com.itextpdf.text.DocumentException;
import com.itextpdf.text.Element;
import com.itextpdf.text.Font;
import com.itextpdf.text.Image;
import com.itextpdf.text.PageSize;
import com.itextpdf.text.Paragraph;

import com.itextpdf.text.pdf.PdfPCell;
import com.itextpdf.text.pdf.PdfPTable;
import com.itextpdf.text.pdf.PdfWriter;


import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;
import java.net.MalformedURLException;
import java.util.ArrayList;
import java.util.logging.Level;
import java.util.logging.Logger;
import javax.swing.JOptionPane;
/**
 *
 * @author INFSOLUTION
 */
public class GeraPdf {
    public static final long serialVersionUID = 3;

    public void geraPdf(String texto, String nome, String nasc,String docType) throws  IOException, DocumentException {
        String hoje="";
        String hoje1="";
        InfclinTools data = new InfclinTools();
        hoje = data.InfclinData();
        hoje1= data.forData();
         
    Document receita = new Document(PageSize.A5,14,14,14,14);
        try {
            
            
            PdfPTable table = new PdfPTable(1);
            table.setWidthPercentage(100.0f);
            table.setHorizontalAlignment(Element.ALIGN_LEFT);
            Font titulo_f = new Font(Font.FontFamily.UNDEFINED,12,Font.BOLD);
            Font medic_f = new Font(Font.FontFamily.UNDEFINED);
            Font clinic_f = new Font(Font.FontFamily.UNDEFINED);
            Font normal_f = new Font(Font.FontFamily.UNDEFINED,7);
            Font negrito_f = new Font(Font.FontFamily.UNDEFINED,7,Font.BOLD);
            Font especi_f = new Font(Font.FontFamily.UNDEFINED,12);
            
          
            PdfPCell cabecalho = new PdfPCell();
            PdfPCell cliente = new PdfPCell();
            PdfPCell titDoc = new PdfPCell();
            PdfPCell corpo = new PdfPCell();
            PdfPCell fim = new PdfPCell();
            Paragraph receit = new Paragraph(texto);
            Paragraph nomeEmpresa = new Paragraph("NOME DA CLINICA",titulo_f);
            Paragraph nomeMedic = new Paragraph("Dr. ************ - CRM ***",medic_f);
            Paragraph  especializa = new Paragraph("CLINICA MÉDICA -  INFECTOLOGIA", clinic_f);
            Paragraph  especialida= new Paragraph("Doenças Infecto-contagiosas, Parasitárias Respiratórias e Clínica Geral.",normal_f);
            Paragraph endereco = new Paragraph("Endereço:**************************.",normal_f);
            Paragraph fone = new Paragraph("Fones: **********************************",normal_f);
            Paragraph local = new Paragraph("Cep:********** Teresina - Piaui",normal_f);
            Paragraph cnpj = new Paragraph("CNPJ:***************",normal_f);
            Paragraph espac = new Paragraph("                ____________________________   ");
            Paragraph espaco = new Paragraph("            ");
            Paragraph diaAssin = new Paragraph(hoje1+"                                        Médico                   ");
            Paragraph name = new Paragraph("Nome: "+nome);
            Paragraph nasci = new Paragraph("Data de nascimento: "+nasc);
            Paragraph documen = new Paragraph(docType);
            nomeEmpresa.setAlignment(Element.ALIGN_CENTER);
            nomeMedic.setAlignment(Element.ALIGN_CENTER);
            especializa.setAlignment(Element.ALIGN_CENTER);
            especialida.setAlignment(Element.ALIGN_CENTER);
            endereco.setAlignment(Element.ALIGN_CENTER);
            fone.setAlignment(Element.ALIGN_CENTER);
            local.setAlignment(Element.ALIGN_CENTER);
            cnpj.setAlignment(Element.ALIGN_CENTER);
            espac.setAlignment(Element.ALIGN_RIGHT);
            diaAssin.setAlignment(Element.ALIGN_CENTER);
            documen.setAlignment(Element.ALIGN_CENTER);
            espac.setAlignment(Element.ALIGN_RIGHT);
            diaAssin.setAlignment(Element.ALIGN_CENTER);
            cabecalho.addElement(nomeEmpresa);
            cabecalho.addElement(nomeMedic);
            cabecalho.addElement(especializa);
            cabecalho.addElement(especialida);
            cabecalho.addElement(endereco);
            cabecalho.addElement(fone);
            cabecalho.addElement(local);
            cabecalho.addElement(cnpj);
            cabecalho.setBorderColor(BaseColor.WHITE);
            cabecalho.setHorizontalAlignment(Element.ALIGN_CENTER);
            cliente.addElement(name);
            cliente.addElement(nasci);
            cliente.setBorderColor(BaseColor.WHITE);
            cliente.setHorizontalAlignment(Element.ALIGN_LEFT);
            titDoc.addElement(documen);
           titDoc.setBorderColor(BaseColor.WHITE);
            titDoc.setHorizontalAlignment(Element.ALIGN_CENTER);
            
            corpo.addElement(receit);
            corpo.setBorderColor(BaseColor.WHITE);
            corpo.setFixedHeight(280f);
            corpo.setHorizontalAlignment(Element.ALIGN_JUSTIFIED);
            fim.addElement(espac);
            fim.addElement(diaAssin);
            fim.setBorderColor(BaseColor.WHITE);
            fim.setHorizontalAlignment(Element.ALIGN_CENTER);
            JOptionPane.showMessageDialog(null, "VAI CRIAR A IMAGEM");
             

            Image infLogoI = Image.getInstance("logoP.png");

            JOptionPane.showMessageDialog(null, "Criou a imagem.");
            infLogoI.setAlignment(Element.ALIGN_CENTER);
            JOptionPane.showMessageDialog(null, "alinhamento.");
            infLogoI.setBorderColor(BaseColor.WHITE);
            JOptionPane.showMessageDialog(null, "base color");
            PdfWriter grave = PdfWriter.getInstance(receita, new FileOutputStream("C:\\infclin1.0\\receituariopdf\\"+nome+hoje+".pdf"));
            receita.open();
            PdfPCell infLogo = new PdfPCell(infLogoI);
            infLogo.setColspan(1);
            infLogo.setBorderColor(BaseColor.WHITE);
            infLogo.setHorizontalAlignment(Element.ALIGN_CENTER);
            table.addCell(infLogo);
            receita.add(infLogo);
            table.addCell(cabecalho);
            table.addCell(cliente);
            table.addCell(titDoc);
            table.addCell(corpo);
            table.addCell(fim);
            receita.add(table);
            receita.close();
        } catch (FileNotFoundException ex) {
            Logger.getLogger(GeraPdf.class.getName()).log(Level.SEVERE, null, ex);
        }
        java.awt.Desktop desktop = java.awt.Desktop.getDesktop();    
        try {   
            desktop.open(new File("C:\\infclin1.0\\receituariopdf\\"+nome+hoje+".pdf"));
        } catch (IOException ex) {
            Logger.getLogger(GeraPdf.class.getName()).log(Level.SEVERE, null, ex);
        }
    }
}
 
