---
title: TextBox Binding in WPF , MVVM
categories:
- WPF
tags:
- WPF
- MVVM-Binding
---

## TextBox LostFocus

### Set the event name of the EventTrigger to LostFocus and pass the Text property as the CommandParameter:
``` bash
  <TextBox x:Name="txt">
      <i:Interaction.Triggers>
          <i:EventTrigger EventName="LostFocus" >
              <i:InvokeCommandAction Command="{Binding YourCommand}" CommandParameter="{Binding Path=Text, ElementName=txt" />
          </i:EventTrigger>
      </i:Interaction.Triggers>
  </TextBox>
``` 

### Example
``` bash
  <Window
          xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
          xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
          xmlns:local="clr-namespace:WpfApplication5"
          xmlns:i="http://schemas.microsoft.com/expression/2010/interactivity" x:Class="WpfApplication5.MainWindow"
          Title="MainWindow" Height="350" Width="525">

      <TextBox HorizontalAlignment="Left" Height="36.667" Margin="116,0,0,0" TextWrapping="Wrap" Text="TextBox" Width="62">
        <i:Interaction.Triggers>
          <i:EventTrigger EventName="LostFocus">
            <i:InvokeCommandAction Command="{Binding WhateverCommand}"/>
          </i:EventTrigger>
        </i:Interaction.Triggers>
      </TextBox>

  </Window>
``` 

## TextBox InputBindings

``` bash
<TextBox x:Name="TextBox1" Height="23" TextWrapping="Wrap"          
         VerticalAlignment="Center" HorizontalAlignment="Stretch" Margin="0,20,20,0">
    <TextBox.InputBindings>
        <KeyBinding Command="{Binding YourCommand}" Key="Enter"></KeyBinding>
    </TextBox.InputBindings>
</TextBox>
``` 

