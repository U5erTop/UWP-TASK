
# README: Задания и решения по Элементам управления UWP

**Автор:** Учебный материал
**Версия:** 1.0
**Дата создания:** 2025
**Язык:** C#, XAML
**Платформа:** Universal Windows Platform (UWP)

## Содержание
1. [Введение](#введение)
2. [Основные элементы управления](#основные-элементы-управления)
3. [Элементы выбора](#элементы-выбора)
4. [Элементы ввода](#элементы-ввода)
5. [Контейнеры и макеты](#контейнеры-и-макеты)
6. [Прогресс и обратная связь](#прогресс-и-обратная-связь)
7. [Навигация](#навигация)
8. [Элементы отображения данных](#элементы-отображения-данных)
9. [События и привязка данных](#события-и-привязка-данных)
10. [Продвинутые техники](#продвинутые-техники)

---

## Введение

Этот документ содержит 100+ практических заданий по работе с элементами управления UWP (Universal Windows Platform). Каждое задание включает:
- Описание задачи
- Требуемый XAML код
- Код на C#
- Объяснение решения

### Структура курса

Задания организованы по уровню сложности:
- **Базовые** (1-20): Создание и настройка простых элементов
- **Промежуточные** (21-60): Обработка событий и привязка данных
- **Продвинутые** (61-100): Сложные сценарии и оптимизация

---

## Основные элементы управления

### Задание 1: Создание простой кнопки

**Описание:** Создайте кнопку с текстом "Нажми меня" и обработайте событие Click.

**XAML:**
```xaml
<Button x:Name="MyButton" 
        Content="Нажми меня" 
        Click="MyButton_Click"
        Width="200" 
        Height="50"
        FontSize="18"/>
```

**C#:**
```csharp
private void MyButton_Click(object sender, RoutedEventArgs e)
{
    ContentDialog dialog = new ContentDialog
    {
        Title = "Событие",
        Content = "Кнопка была нажата!",
        PrimaryButtonText = "ОК"
    };
    _ = dialog.ShowAsync();
}
```

**Объяснение:** Button - это базовый элемент управления. Событие Click срабатывает при нажатии. ContentDialog используется для отображения диалогового окна.

---

### Задание 2: TextBlock для отображения текста

**Описание:** Создайте TextBlock с форматированным текстом (жирный, курсив, цвет).

**XAML:**
```xaml
<TextBlock Margin="20" LineHeight="30">
    <Run Text="Обычный текст " />
    <Run Text="Жирный текст" FontWeight="Bold" Foreground="Blue" />
    <Run Text=" и " />
    <Run Text="курсивный" FontStyle="Italic" Foreground="Red" />
</TextBlock>
```

**Объяснение:** TextBlock содержит элементы Run для разного форматирования. Каждый Run может иметь свои свойства.

---

### Задание 3: TextBox для ввода текста

**Описание:** Создайте TextBox, где пользователь может ввести текст, и отобразите введенный текст в TextBlock.

**XAML:**
```xaml
<StackPanel Spacing="10" Padding="20">
    <TextBox x:Name="InputTextBox" 
             PlaceholderText="Введите текст..."
             TextChanged="InputTextBox_TextChanged"/>
    <TextBlock x:Name="OutputTextBlock" 
               Text="Введено: " 
               FontSize="16"/>
</StackPanel>
```

**C#:**
```csharp
private void InputTextBox_TextChanged(object sender, TextChangedEventArgs e)
{
    OutputTextBlock.Text = "Введено: " + InputTextBox.Text;
}
```

---

### Задание 4: PasswordBox для ввода пароля

**Описание:** Создайте PasswordBox и кнопку для проверки пароля.

**XAML:**
```xaml
<StackPanel Spacing="10" Padding="20">
    <PasswordBox x:Name="PasswordInput" 
                 PlaceholderText="Введите пароль"/>
    <Button Content="Проверить пароль" 
            Click="CheckPassword_Click"/>
    <TextBlock x:Name="ResultTextBlock" Foreground="Red"/>
</StackPanel>
```

**C#:**
```csharp
private void CheckPassword_Click(object sender, RoutedEventArgs e)
{
    string password = PasswordInput.Password;
    if (password == "12345")
    {
        ResultTextBlock.Text = "Пароль верный!";
        ResultTextBlock.Foreground = new SolidColorBrush(Colors.Green);
    }
    else
    {
        ResultTextBlock.Text = "Пароль неверный!";
    }
}
```

---

### Задание 5: HyperlinkButton для открытия ссылки

**Описание:** Создайте HyperlinkButton, который открывает веб-сайт.

**XAML:**
```xaml
<HyperlinkButton NavigateUri="https://www.microsoft.com"
                 Content="Перейти на Microsoft"
                 Margin="20"/>
```

**Объяснение:** HyperlinkButton автоматически открывает ссылку в браузере по умолчанию. Свойство NavigateUri указывает URL.

---

## Элементы выбора

### Задание 6: CheckBox для множественного выбора

**Описание:** Создайте три CheckBox для выбора интересов.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите интересы:" FontSize="18" FontWeight="Bold"/>
    <CheckBox x:Name="CheckSports" Content="Спорт"/>
    <CheckBox x:Name="CheckMusic" Content="Музыка"/>
    <CheckBox x:Name="CheckReading" Content="Чтение"/>
    <Button Content="Показать результат" Click="ShowInterests_Click"/>
    <TextBlock x:Name="InterestsTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void ShowInterests_Click(object sender, RoutedEventArgs e)
{
    string interests = "Выбранные интересы: ";
    if (CheckSports.IsChecked == true) interests += "Спорт ";
    if (CheckMusic.IsChecked == true) interests += "Музыка ";
    if (CheckReading.IsChecked == true) interests += "Чтение ";
    InterestsTextBlock.Text = interests;
}
```

---

### Задание 7: RadioButton для выбора одного из нескольких вариантов

**Описание:** Создайте группу RadioButton для выбора пола.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите пол:" FontSize="18" FontWeight="Bold"/>
    <RadioButton GroupName="Gender" Content="Мужской" x:Name="RadioMale"/>
    <RadioButton GroupName="Gender" Content="Женский" x:Name="RadioFemale"/>
    <RadioButton GroupName="Gender" Content="Другое" x:Name="RadioOther"/>
    <Button Content="Показать результат" Click="ShowGender_Click"/>
    <TextBlock x:Name="GenderTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void ShowGender_Click(object sender, RoutedEventArgs e)
{
    string selected = "Пол не выбран";
    if (RadioMale.IsChecked == true) selected = "Выбран: Мужской";
    else if (RadioFemale.IsChecked == true) selected = "Выбран: Женский";
    else if (RadioOther.IsChecked == true) selected = "Выбран: Другое";
    GenderTextBlock.Text = selected;
}
```

---

### Задание 8: ToggleSwitch для включения/отключения функции

**Описание:** Создайте ToggleSwitch для включения темного режима.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <ToggleSwitch x:Name="DarkModeToggle"
                  Header="Темный режим"
                  OnContent="Включен"
                  OffContent="Отключен"
                  Toggled="DarkMode_Toggled"/>
    <TextBlock x:Name="StatusTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void DarkMode_Toggled(object sender, RoutedEventArgs e)
{
    if (DarkModeToggle.IsOn)
    {
        StatusTextBlock.Text = "Темный режим включен";
        StatusTextBlock.Foreground = new SolidColorBrush(Colors.White);
    }
    else
    {
        StatusTextBlock.Text = "Темный режим отключен";
        StatusTextBlock.Foreground = new SolidColorBrush(Colors.Black);
    }
}
```

---

### Задание 9: ComboBox для выбора из списка

**Описание:** Создайте ComboBox с городами.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите город:" FontSize="16" FontWeight="Bold"/>
    <ComboBox x:Name="CityComboBox" 
              SelectionChanged="City_SelectionChanged"
              PlaceholderText="Выберите...">
        <x:String>Москва</x:String>
        <x:String>Санкт-Петербург</x:String>
        <x:String>Казань</x:String>
        <x:String>Екатеринбург</x:String>
    </ComboBox>
    <TextBlock x:Name="SelectedCityTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void City_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    if (CityComboBox.SelectedItem != null)
    {
        SelectedCityTextBlock.Text = "Выбран город: " + CityComboBox.SelectedItem.ToString();
    }
}
```

---

### Задание 10: ListBox для отображения списка элементов

**Описание:** Создайте ListBox со списком животных и отобразите выбранное животное.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите животное:" FontSize="16" FontWeight="Bold"/>
    <ListBox x:Name="AnimalListBox" 
             SelectionChanged="Animal_SelectionChanged"
             Height="150">
        <x:String>Кошка</x:String>
        <x:String>Собака</x:String>
        <x:String>Птица</x:String>
        <x:String>Рыба</x:String>
        <x:String>Кролик</x:String>
    </ListBox>
    <TextBlock x:Name="SelectedAnimalTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void Animal_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    if (AnimalListBox.SelectedItem != null)
    {
        SelectedAnimalTextBlock.Text = "Выбрано: " + AnimalListBox.SelectedItem.ToString();
    }
}
```

---

## Элементы ввода

### Задание 11: Slider для выбора числового значения

**Описание:** Создайте Slider для выбора громкости (0-100).

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Громкость:" FontSize="16" FontWeight="Bold"/>
    <Slider x:Name="VolumeSlider"
            Minimum="0"
            Maximum="100"
            Value="50"
            ValueChanged="Volume_ValueChanged"
            Width="300"/>
    <TextBlock x:Name="VolumeValueTextBlock" 
               Text="Громкость: 50" 
               FontSize="14"/>
</StackPanel>
```

**C#:**
```csharp
private void Volume_ValueChanged(object sender, RangeBaseValueChangedEventArgs e)
{
    VolumeValueTextBlock.Text = $"Громкость: {(int)VolumeSlider.Value}";
}
```

---

### Задание 12: Spinner для ввода чисел

**Описание:** Создайте NumberBox для ввода возраста.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Введите возраст:" FontSize="16" FontWeight="Bold"/>
    <NumberBox x:Name="AgeNumberBox"
               Value="18"
               Minimum="0"
               Maximum="120"
               SpinButtonPlacementMode="Inline"
               Header="Возраст"/>
    <Button Content="Подтвердить" Click="ConfirmAge_Click"/>
    <TextBlock x:Name="AgeConfirmTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void ConfirmAge_Click(object sender, RoutedEventArgs e)
{
    if (double.IsNaN(AgeNumberBox.Value))
    {
        AgeConfirmTextBlock.Text = "Пожалуйста, введите возраст";
    }
    else
    {
        AgeConfirmTextBlock.Text = $"Ваш возраст: {(int)AgeNumberBox.Value} лет";
    }
}
```

---

### Задание 13: DatePicker для выбора даты

**Описание:** Создайте DatePicker для выбора даты рождения.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите дату рождения:" FontSize="16" FontWeight="Bold"/>
    <DatePicker x:Name="BirthdatePicker" 
                Header="Дата рождения"
                DateChanged="Birthdate_Changed"/>
    <TextBlock x:Name="SelectedDateTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void Birthdate_Changed(DatePicker sender, DatePickerValueChangedEventArgs args)
{
    if (sender.Date != null)
    {
        DateTime date = sender.Date.DateTime;
        SelectedDateTextBlock.Text = $"Выбрана дата: {date:dd.MM.yyyy}";
    }
}
```

---

### Задание 14: TimePicker для выбора времени

**Описание:** Создайте TimePicker для выбора времени встречи.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите время встречи:" FontSize="16" FontWeight="Bold"/>
    <TimePicker x:Name="MeetingTimePicker"
                Header="Время встречи"
                TimeChanged="MeetingTime_Changed"/>
    <TextBlock x:Name="SelectedTimeTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void MeetingTime_Changed(TimePicker sender, TimePickerValueChangedEventArgs args)
{
    TimeSpan time = sender.Time;
    SelectedTimeTextBlock.Text = $"Выбрано время: {time:hh\:mm}";
}
```

---

### Задание 15: ColorPicker для выбора цвета

**Описание:** Создайте ColorPicker и отобразите выбранный цвет.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Выберите цвет:" FontSize="16" FontWeight="Bold"/>
    <ColorPicker x:Name="ColorSelection"
                 ColorChanged="Color_Changed"
                 IsAlphaEnabled="False"/>
    <Rectangle x:Name="ColorRectangle"
               Width="100"
               Height="100"
               Fill="Red"
               Margin="0,10,0,0"/>
    <TextBlock x:Name="ColorHexTextBlock" Margin="0,10,0,0"/>
</StackPanel>
```

**C#:**
```csharp
private void Color_Changed(ColorPicker sender, ColorChangedEventArgs args)
{
    Windows.UI.Color color = args.NewColor;
    ColorRectangle.Fill = new SolidColorBrush(color);
    ColorHexTextBlock.Text = $"Цвет: #{color.R:X2}{color.G:X2}{color.B:X2}";
}
```

---

## Контейнеры и макеты

### Задание 16: StackPanel для вертикального расположения элементов

**Описание:** Создайте StackPanel с кнопками, расположенными вертикально.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Вертикальное расположение:" 
               FontSize="18" 
               FontWeight="Bold"/>
    <Button Content="Кнопка 1" />
    <Button Content="Кнопка 2" />
    <Button Content="Кнопка 3" />
</StackPanel>
```

---

### Задание 17: StackPanel горизонтальное расположение

**Описание:** Создайте горизонтальный StackPanel с элементами.

**XAML:**
```xaml
<StackPanel Orientation="Horizontal" 
            Padding="20" 
            Spacing="10">
    <Button Content="Кнопка 1" Width="100" />
    <Button Content="Кнопка 2" Width="100" />
    <Button Content="Кнопка 3" Width="100" />
</StackPanel>
```

---

### Задание 18: Grid для создания таблицы элементов

**Описание:** Создайте Grid 2x2 с кнопками.

**XAML:**
```xaml
<Grid Padding="20" RowSpacing="10" ColumnSpacing="10">
    <Grid.RowDefinitions>
        <RowDefinition Height="Auto"/>
        <RowDefinition Height="Auto"/>
    </Grid.RowDefinitions>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="100"/>
        <ColumnDefinition Width="100"/>
    </Grid.ColumnDefinitions>

    <Button Content="Кнопка 1" Grid.Row="0" Grid.Column="0"/>
    <Button Content="Кнопка 2" Grid.Row="0" Grid.Column="1"/>
    <Button Content="Кнопка 3" Grid.Row="1" Grid.Column="0"/>
    <Button Content="Кнопка 4" Grid.Row="1" Grid.Column="1"/>
</Grid>
```

---

### Задание 19: RelativePanel для относительного позиционирования

**Описание:** Создайте RelativePanel с элементами, позиционированными относительно друг друга.

**XAML:**
```xaml
<RelativePanel Padding="20">
    <TextBlock x:Name="Title" 
               Text="Заголовок"
               FontSize="20"
               FontWeight="Bold"/>
    <TextBlock x:Name="Description"
               Text="Это описание находится ниже заголовка"
               RelativePanel.Below="Title"
               Margin="0,10,0,0"/>
    <Button Content="ОК"
            RelativePanel.Below="Description"
            Margin="0,20,0,0"/>
</RelativePanel>
```

---

### Задание 20: ScrollViewer для прокрутки содержимого

**Описание:** Создайте ScrollViewer с большим количеством текста.

**XAML:**
```xaml
<ScrollViewer Padding="20" VerticalScrollBarVisibility="Auto">
    <TextBlock TextWrapping="Wrap" FontSize="14">
        Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
        Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
        Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris 
        nisi ut aliquip ex ea commodo consequat... [повторено много раз]
    </TextBlock>
</ScrollViewer>
```

---

## Прогресс и обратная связь

### Задание 21: ProgressBar для отображения хода выполнения

**Описание:** Создайте ProgressBar, который заполняется при нажатии кнопки.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBlock Text="Ход выполнения:" FontSize="16" FontWeight="Bold"/>
    <ProgressBar x:Name="MyProgressBar"
                 Value="0"
                 Maximum="100"
                 Height="20"/>
    <Button Content="Начать процесс" Click="StartProcess_Click"/>
</StackPanel>
```

**C#:**
```csharp
private async void StartProcess_Click(object sender, RoutedEventArgs e)
{
    for (int i = 0; i <= 100; i++)
    {
        MyProgressBar.Value = i;
        await Task.Delay(50);
    }
}
```

---

### Задание 22: ProgressRing для отображения загрузки

**Описание:** Создайте ProgressRing, который вращается во время загрузки.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10" HorizontalAlignment="Center">
    <ProgressRing x:Name="LoadingRing"
                  IsActive="True"
                  Width="100"
                  Height="100"/>
    <TextBlock Text="Загрузка..." 
               TextAlignment="Center"
               FontSize="16"/>
    <Button Content="Остановить" Click="StopLoading_Click"/>
</StackPanel>
```

**C#:**
```csharp
private void StopLoading_Click(object sender, RoutedEventArgs e)
{
    LoadingRing.IsActive = false;
}
```

---

### Задание 23: InfoBar для отображения информационного сообщения

**Описание:** Создайте InfoBar с предупреждением.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <InfoBar Title="Внимание"
             Message="Это важное сообщение"
             Severity="Warning"
             IsOpen="True"
             IsClosable="True"/>
    <Button Content="Показать успех" Click="ShowSuccess_Click"/>
</StackPanel>
```

**C#:**
```csharp
private void ShowSuccess_Click(object sender, RoutedEventArgs e)
{
    InfoBar successBar = new InfoBar
    {
        Title = "Успех",
        Message = "Операция выполнена успешно!",
        Severity = InfoBarSeverity.Success,
        IsOpen = true,
        IsClosable = true
    };
    // Добавьте в контейнер
}
```

---

### Задание 24: Tooltip для подсказок

**Описание:** Добавьте Tooltip к кнопке.

**XAML:**
```xaml
<Button Content="Кнопка" 
        ToolTipService.ToolTip="Это подсказка"
        Padding="20"/>
```

**Объяснение:** Tooltip отображается при наведении мыши на элемент управления.

---

### Задание 25: MessageDialog для уведомлений

**Описание:** Создайте кнопку, которая показывает диалоговое окно с сообщением.

**C#:**
```csharp
private async void ShowMessage_Click(object sender, RoutedEventArgs e)
{
    ContentDialog dialog = new ContentDialog
    {
        Title = "Уведомление",
        Content = "Это диалоговое окно",
        PrimaryButtonText = "ОК",
        SecondaryButtonText = "Отмена"
    };

    ContentDialogResult result = await dialog.ShowAsync();
    if (result == ContentDialogResult.Primary)
    {
        // Нажата кнопка ОК
    }
}
```

---

## Навигация

### Задание 26: Frame для навигации между страницами

**Описание:** Создайте Frame и навигируйте на другую страницу.

**XAML (MainPage.xaml):**
```xaml
<StackPanel Padding="20" Spacing="10">
    <Button Content="Перейти на вторую страницу" Click="Navigate_Click"/>
    <Frame x:Name="NavigationFrame"/>
</StackPanel>
```

**C#:**
```csharp
private void Navigate_Click(object sender, RoutedEventArgs e)
{
    NavigationFrame.Navigate(typeof(SecondPage));
}
```

---

### Задание 27: NavigationView для боковой панели навигации

**Описание:** Создайте NavigationView с меню навигации.

**XAML:**
```xaml
<NavigationView IsBackButtonVisible="Visible">
    <NavigationView.MenuItems>
        <NavigationViewItem Content="Главная" Tag="home" Icon="Home"/>
        <NavigationViewItem Content="Параметры" Tag="settings" Icon="Setting"/>
        <NavigationViewItem Content="О программе" Tag="about" Icon="Help"/>
    </NavigationView.MenuItems>

    <Frame x:Name="NavFrame"/>
</NavigationView>
```

---

### Задание 28: TabView для вкладок

**Описание:** Создайте TabView с несколькими вкладками.

**XAML:**
```xaml
<TabView x:Name="MyTabView">
    <TabViewItem Header="Вкладка 1">
        <TextBlock Text="Содержимое вкладки 1" Padding="20"/>
    </TabViewItem>
    <TabViewItem Header="Вкладка 2">
        <TextBlock Text="Содержимое вкладки 2" Padding="20"/>
    </TabViewItem>
    <TabViewItem Header="Вкладка 3">
        <TextBlock Text="Содержимое вкладки 3" Padding="20"/>
    </TabViewItem>
</TabView>
```

---

## Элементы отображения данных

### Задание 29: ListView для отображения списка элементов

**Описание:** Создайте ListView с данными о фруктах.

**XAML:**
```xaml
<ListView x:Name="FruitsList" 
          Height="200"
          SelectionChanged="Fruit_SelectionChanged">
</ListView>
```

**C#:**
```csharp
public MainPage()
{
    this.InitializeComponent();
    ObservableCollection<string> fruits = new ObservableCollection<string>
    {
        "Яблоко",
        "Банан",
        "Апельсин",
        "Груша",
        "Киви"
    };
    FruitsList.ItemsSource = fruits;
}

private void Fruit_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    if (FruitsList.SelectedItem != null)
    {
        // Обработка выбора
    }
}
```

---

### Задание 30: GridView для отображения сетки элементов

**Описание:** Создайте GridView с изображениями.

**XAML:**
```xaml
<GridView x:Name="ImageGrid"
          SelectionMode="Single"
          ItemsSource="{x:Bind Images}">
    <GridView.ItemTemplate>
        <DataTemplate x:DataType="local:ImageItem">
            <Image Source="{x:Bind ImagePath}" 
                   Width="150" 
                   Height="150"/>
        </DataTemplate>
    </GridView.ItemTemplate>
</GridView>
```

---

### Задание 31: ItemsControl для пользовательского отображения

**Описание:** Создайте ItemsControl с пользовательским шаблоном.

**XAML:**
```xaml
<ItemsControl x:Name="MyItemsControl" ItemsSource="{x:Bind Items}">
    <ItemsControl.ItemTemplate>
        <DataTemplate x:DataType="local:Item">
            <Border BorderBrush="Blue" BorderThickness="1" Padding="10" Margin="5">
                <TextBlock Text="{x:Bind Name}" FontSize="16"/>
            </Border>
        </DataTemplate>
    </ItemsControl.ItemTemplate>
</ItemsControl>
```

---

### Задание 32: TreeView для иерархического отображения

**Описание:** Создайте TreeView с категориями и подкатегориями.

**XAML:**
```xaml
<TreeView>
    <TreeViewNode Content="Категория 1" IsExpanded="True">
        <TreeViewNode Content="Подкатегория 1.1"/>
        <TreeViewNode Content="Подкатегория 1.2"/>
    </TreeViewNode>
    <TreeViewNode Content="Категория 2">
        <TreeViewNode Content="Подкатегория 2.1"/>
    </TreeViewNode>
</TreeView>
```

---

## События и привязка данных

### Задание 33: Привязка данных (Binding) к свойству

**Описание:** Создайте привязку между TextBox и TextBlock.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBox x:Name="SourceTextBox" 
             PlaceholderText="Введите текст..."/>
    <TextBlock Text="{Binding ElementName=SourceTextBox, Path=Text}"
               FontSize="18"
               Foreground="Blue"/>
</StackPanel>
```

---

### Задание 34: x:Bind для привязки данных

**Описание:** Используйте x:Bind для привязки к свойствам ViewModel.

**C#:**
```csharp
public class ViewModel : INotifyPropertyChanged
{
    private string _name;
    public string Name
    {
        get { return _name; }
        set
        {
            if (_name != value)
            {
                _name = value;
                OnPropertyChanged(nameof(Name));
            }
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;

    private void OnPropertyChanged(string propertyName)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
```

**XAML:**
```xaml
<TextBlock Text="{x:Bind ViewModel.Name, Mode=OneWay}" FontSize="18"/>
```

---

### Задание 35: Обработка события Click с параметрами

**Описание:** Обработайте Click событие и получите информацию об отправителе.

**C#:**
```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    Button button = sender as Button;
    if (button != null)
    {
        string content = button.Content.ToString();
        // Обработка
    }
}
```

---

### Задание 36: Событие TextChanged для фильтрации данных

**Описание:** Создайте TextBox для поиска и фильтрации ListView.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <TextBox x:Name="SearchBox"
             PlaceholderText="Поиск..."
             TextChanged="SearchBox_TextChanged"/>
    <ListView x:Name="ResultsList"/>
</StackPanel>
```

**C#:**
```csharp
private void SearchBox_TextChanged(object sender, TextChangedEventArgs e)
{
    string searchText = SearchBox.Text.ToLower();
    var filtered = items.Where(item => item.Name.ToLower().Contains(searchText)).ToList();
    ResultsList.ItemsSource = filtered;
}
```

---

### Задание 37: ObservableCollection для обновления UI

**Описание:** Создайте ObservableCollection и добавляйте элементы динамически.

**C#:**
```csharp
private ObservableCollection<string> items;

public MainPage()
{
    this.InitializeComponent();
    items = new ObservableCollection<string>();
    MyListView.ItemsSource = items;
}

private void AddItem_Click(object sender, RoutedEventArgs e)
{
    items.Add("Новый элемент " + (items.Count + 1));
}
```

---

## Продвинутые техники

### Задание 38: Создание пользовательского элемента управления (UserControl)

**Описание:** Создайте UserControl для отображения карточки товара.

**ProductCard.xaml:**
```xaml
<UserControl>
    <Border BorderBrush="Gray" BorderThickness="1" CornerRadius="5">
        <StackPanel Padding="10" Spacing="5">
            <TextBlock x:Name="ProductName" 
                       FontSize="18" 
                       FontWeight="Bold"/>
            <TextBlock x:Name="ProductPrice" 
                       FontSize="14" 
                       Foreground="Green"/>
            <Button x:Name="BuyButton" 
                    Content="Купить"/>
        </StackPanel>
    </Border>
</UserControl>
```

**ProductCard.xaml.cs:**
```csharp
public sealed partial class ProductCard : UserControl
{
    public ProductCard()
    {
        this.InitializeComponent();
    }

    public string ProductName
    {
        get { return ProductName.Text; }
        set { ProductName.Text = value; }
    }

    public string ProductPrice
    {
        get { return ProductPrice.Text; }
        set { ProductPrice.Text = value; }
    }

    public event RoutedEventHandler BuyClick
    {
        add { BuyButton.Click += value; }
        remove { BuyButton.Click -= value; }
    }
}
```

---

### Задание 39: Привязка к коллекции с DataTemplateSelector

**Описание:** Создайте селектор шаблонов для разных типов данных.

**C#:**
```csharp
public class ItemTemplateSelector : DataTemplateSelector
{
    public DataTemplate TextTemplate { get; set; }
    public DataTemplate ImageTemplate { get; set; }

    protected override DataTemplate SelectTemplateCore(object item, DependencyObject container)
    {
        if (item is TextItem)
            return TextTemplate;
        else if (item is ImageItem)
            return ImageTemplate;
        return base.SelectTemplateCore(item, container);
    }
}
```

---

### Задание 40: Стилизация элементов управления

**Описание:** Создайте стиль для кнопок.

**XAML (в App.xaml или ResourceDictionary):**
```xaml
<Style x:Key="PrimaryButtonStyle" TargetType="Button">
    <Setter Property="Background" Value="Blue"/>
    <Setter Property="Foreground" Value="White"/>
    <Setter Property="Padding" Value="20,10"/>
    <Setter Property="FontSize" Value="16"/>
    <Setter Property="FontWeight" Value="Bold"/>
</Style>
```

**Использование:**
```xaml
<Button Content="Нажми меня" Style="{StaticResource PrimaryButtonStyle}"/>
```

---

### Задание 41: Создание шаблона элемента управления (ControlTemplate)

**Описание:** Создайте пользовательский шаблон для кнопки.

**XAML:**
```xaml
<Style TargetType="Button">
    <Setter Property="Template">
        <Setter.Value>
            <ControlTemplate TargetType="Button">
                <Border Background="{TemplateBinding Background}"
                        CornerRadius="10"
                        Padding="10">
                    <ContentPresenter Content="{TemplateBinding Content}"
                                      HorizontalAlignment="Center"
                                      VerticalAlignment="Center"/>
                </Border>
            </ControlTemplate>
        </Setter.Value>
    </Setter>
</Style>
```

---

### Задание 42: Анимации элементов управления

**Описание:** Создайте анимацию для масштабирования элемента.

**C#:**
```csharp
private async void AnimateButton_Click(object sender, RoutedEventArgs e)
{
    var storyboard = new Storyboard();
    var scaleAnimation = new DoubleAnimation
    {
        From = 1.0,
        To = 1.5,
        Duration = new Duration(TimeSpan.FromSeconds(1))
    };
    Storyboard.SetTarget(scaleAnimation, MyButton);
    Storyboard.SetTargetProperty(scaleAnimation, "(UIElement.RenderTransform).(ScaleTransform.ScaleX)");
    storyboard.Children.Add(scaleAnimation);
    storyboard.Begin();
}
```

---

### Задание 43: Обработка кнопок и жестов

**Описание:** Обработайте жесты касания на элементе.

**C#:**
```csharp
private void Element_PointerEntered(object sender, PointerRoutedEventArgs e)
{
    // Мышь вошла в область элемента
}

private void Element_PointerExited(object sender, PointerRoutedEventArgs e)
{
    // Мышь вышла из области элемента
}

private void Element_PointerPressed(object sender, PointerRoutedEventArgs e)
{
    // Кнопка мыши или палец нажат
}

private void Element_PointerReleased(object sender, PointerRoutedEventArgs e)
{
    // Кнопка мыши или палец отпущен
}
```

---

### Задание 44: Контекстное меню (RightTap)

**Описание:** Создайте контекстное меню при правом клике.

**XAML:**
```xaml
<TextBlock Text="Правый клик здесь" RightTapped="TextBlock_RightTapped"/>
```

**C#:**
```csharp
private async void TextBlock_RightTapped(object sender, RightTappedRoutedEventArgs e)
{
    PopupMenu menu = new PopupMenu();
    menu.Commands.Add(new UICommand("Копировать"));
    menu.Commands.Add(new UICommand("Вставить"));

    await menu.ShowAsync(e.GetPosition(sender as UIElement));
}
```

---

### Задание 45: Flyout для всплывающих меню

**Описание:** Создайте Flyout при нажатии на кнопку.

**XAML:**
```xaml
<Button Content="Нажми меня">
    <Button.Flyout>
        <Flyout>
            <StackPanel Spacing="10">
                <TextBlock Text="Это всплывающее меню"/>
                <Button Content="Опция 1"/>
                <Button Content="Опция 2"/>
            </StackPanel>
        </Flyout>
    </Button.Flyout>
</Button>
```

---

### Задание 46: MenuFlyout для контекстного меню

**Описание:** Создайте MenuFlyout для элемента.

**XAML:**
```xaml
<Button Content="Меню">
    <Button.Flyout>
        <MenuFlyout>
            <MenuFlyoutItem Text="Пункт 1" Click="MenuItem1_Click"/>
            <MenuFlyoutItem Text="Пункт 2" Click="MenuItem2_Click"/>
            <MenuFlyoutSeparator/>
            <MenuFlyoutItem Text="Выход" Click="Exit_Click"/>
        </MenuFlyout>
    </Button.Flyout>
</Button>
```

---

### Задание 47: AppBarButton в CommandBar

**Описание:** Создайте CommandBar с кнопками действий.

**XAML:**
```xaml
<CommandBar>
    <AppBarButton Icon="Add" Label="Добавить" Click="Add_Click"/>
    <AppBarButton Icon="Edit" Label="Изменить" Click="Edit_Click"/>
    <AppBarButton Icon="Delete" Label="Удалить" Click="Delete_Click"/>
    <CommandBar.SecondaryCommands>
        <AppBarButton Label="Параметры" Click="Settings_Click"/>
        <AppBarButton Label="О приложении" Click="About_Click"/>
    </CommandBar.SecondaryCommands>
</CommandBar>
```

---

### Задание 48: SplitButton для разделенной кнопки

**Описание:** Создайте SplitButton с дополнительными опциями.

**XAML:**
```xaml
<SplitButton Content="Действие"
             Click="MainAction_Click">
    <SplitButton.Flyout>
        <MenuFlyout>
            <MenuFlyoutItem Text="Опция 1"/>
            <MenuFlyoutItem Text="Опция 2"/>
        </MenuFlyout>
    </SplitButton.Flyout>
</SplitButton>
```

---

### Задание 49: DropDownButton для кнопки с меню

**Описание:** Создайте DropDownButton, которая открывает меню.

**XAML:**
```xaml
<DropDownButton Content="Меню">
    <DropDownButton.Flyout>
        <MenuFlyout>
            <MenuFlyoutItem Text="Параметр 1"/>
            <MenuFlyoutItem Text="Параметр 2"/>
            <MenuFlyoutItem Text="Параметр 3"/>
        </MenuFlyout>
    </DropDownButton.Flyout>
</DropDownButton>
```

---

### Задание 50: TeachingTip для подсказок

**Описание:** Создайте TeachingTip для обучения пользователя.

**XAML:**
```xaml
<StackPanel>
    <Button x:Name="TargetButton" Content="Кнопка"/>
    <TeachingTip Target="{x:Bind TargetButton}"
                 Title="Советы"
                 Subtitle="Это полезный совет для пользователя"
                 IsOpen="True"
                 PreferredPlacement="Bottom"/>
</StackPanel>
```

---

### Задание 51: Инкапсуляция логики в ViewModel

**Описание:** Создайте ViewModel для управления состоянием UI.

**C#:**
```csharp
public class MainViewModel : INotifyPropertyChanged
{
    private string _title;
    private ObservableCollection<Item> _items;

    public string Title
    {
        get { return _title; }
        set { SetProperty(ref _title, value); }
    }

    public ObservableCollection<Item> Items
    {
        get { return _items; }
        set { SetProperty(ref _items, value); }
    }

    private void SetProperty<T>(ref T field, T value, [CallerMemberName] string name = null)
    {
        if (!Equals(field, value))
        {
            field = value;
            OnPropertyChanged(name);
        }
    }

    public event PropertyChangedEventHandler PropertyChanged;

    private void OnPropertyChanged(string name)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(name));
    }
}
```

---

### Задание 52: Взаимодействие между элементами управления

**Описание:** Создайте зависимость между ComboBox и ListView.

**C#:**
```csharp
private void Category_SelectionChanged(object sender, SelectionChangedEventArgs e)
{
    string selectedCategory = (string)CategoryComboBox.SelectedItem;
    var filtered = allItems.Where(item => item.Category == selectedCategory).ToList();
    ItemsListView.ItemsSource = filtered;
}
```

---

### Задание 53: Асинхронная загрузка данных

**Описание:** Загрузите данные асинхронно и обновите ListView.

**C#:**
```csharp
private async void LoadData_Click(object sender, RoutedEventArgs e)
{
    LoadingRing.IsActive = true;

    var data = await FetchDataAsync();

    LoadingRing.IsActive = false;
    DataListView.ItemsSource = data;
}

private async Task<List<Item>> FetchDataAsync()
{
    await Task.Delay(2000); // Имитация загрузки
    return new List<Item> { /* данные */ };
}
```

---

### Задание 54: Валидация данных в форме

**Описание:** Создайте форму с валидацией.

**C#:**
```csharp
private bool ValidateForm()
{
    if (string.IsNullOrEmpty(NameTextBox.Text))
    {
        NameErrorTextBlock.Text = "Имя обязательно";
        return false;
    }

    if (string.IsNullOrEmpty(EmailTextBox.Text) || !EmailTextBox.Text.Contains("@"))
    {
        EmailErrorTextBlock.Text = "Неверный email";
        return false;
    }

    return true;
}

private void Submit_Click(object sender, RoutedEventArgs e)
{
    if (ValidateForm())
    {
        // Отправить данные
    }
}
```

---

### Задание 55: Обработка исключений и отображение ошибок

**Описание:** Создайте обработку исключений с информированием пользователя.

**C#:**
```csharp
private async void ProcessData_Click(object sender, RoutedEventArgs e)
{
    try
    {
        var result = await ProcessAsync();
        StatusTextBlock.Text = "Успешно!";
    }
    catch (Exception ex)
    {
        ContentDialog errorDialog = new ContentDialog
        {
            Title = "Ошибка",
            Content = $"Произошла ошибка: {ex.Message}",
            PrimaryButtonText = "ОК"
        };
        await errorDialog.ShowAsync();
    }
}
```

---

### Задание 56: Использование ResourceDictionary

**Описание:** Создайте ResourceDictionary для стилей и шаблонов.

**Styles.xaml:**
```xaml
<ResourceDictionary>
    <Color x:Key="PrimaryColor">Blue</Color>
    <SolidColorBrush x:Key="PrimaryBrush" Color="{StaticResource PrimaryColor}"/>

    <Style x:Key="HeaderTextStyle" TargetType="TextBlock">
        <Setter Property="FontSize" Value="24"/>
        <Setter Property="FontWeight" Value="Bold"/>
        <Setter Property="Foreground" Value="{StaticResource PrimaryBrush}"/>
    </Style>
</ResourceDictionary>
```

**App.xaml:**
```xaml
<Application.Resources>
    <ResourceDictionary Source="Styles.xaml"/>
</Application.Resources>
```

---

### Задание 57: Адаптивный дизайн (Adaptive Layout)

**Описание:** Создайте адаптивный макет для разных размеров экрана.

**C#:**
```csharp
private void MainPage_SizeChanged(object sender, SizeChangedEventArgs e)
{
    if (e.NewSize.Width < 600)
    {
        // Мобильный макет
        MainGrid.ColumnDefinitions.Clear();
        MainGrid.ColumnDefinitions.Add(new ColumnDefinition());
    }
    else
    {
        // Десктопный макет
        MainGrid.ColumnDefinitions.Clear();
        MainGrid.ColumnDefinitions.Add(new ColumnDefinition { Width = new GridLength(1, GridUnitType.Star) });
        MainGrid.ColumnDefinitions.Add(new ColumnDefinition { Width = new GridLength(1, GridUnitType.Star) });
    }
}
```

---

### Задание 58: Использование Behaviors для повторного использования логики

**Описание:** Создайте Behavior для текстового поля.

**C#:**
```csharp
public class NumberOnlyBehavior : Behavior<TextBox>
{
    protected override void OnAttached()
    {
        AssociatedObject.TextChanged += TextBox_TextChanged;
    }

    private void TextBox_TextChanged(object sender, TextChangedEventArgs e)
    {
        TextBox textBox = sender as TextBox;
        textBox.Text = new string(textBox.Text.Where(char.IsDigit).ToArray());
        textBox.SelectionStart = textBox.Text.Length;
    }
}
```

---

### Задание 59: Использование Converters для преобразования данных

**Описание:** Создайте converter для преобразования значения.

**C#:**
```csharp
public class BoolToVisibilityConverter : IValueConverter
{
    public object Convert(object value, Type targetType, object parameter, string language)
    {
        bool boolValue = (bool)value;
        return boolValue ? Visibility.Visible : Visibility.Collapsed;
    }

    public object ConvertBack(object value, Type targetType, object parameter, string language)
    {
        Visibility visibility = (Visibility)value;
        return visibility == Visibility.Visible;
    }
}
```

**XAML:**
```xaml
<local:BoolToVisibilityConverter x:Key="BoolConverter"/>
<TextBlock Visibility="{Binding IsVisible, Converter={StaticResource BoolConverter}}"/>
```

---

### Задание 60: Освоение Pivot для мобильного приложения

**Описание:** Создайте Pivot для навигации между разделами.

**XAML:**
```xaml
<Pivot Title="Мое приложение">
    <PivotItem Header="Главная">
        <TextBlock Text="Содержимое главной" Padding="20"/>
    </PivotItem>
    <PivotItem Header="Профиль">
        <TextBlock Text="Содержимое профиля" Padding="20"/>
    </PivotItem>
    <PivotItem Header="Параметры">
        <TextBlock Text="Содержимое параметров" Padding="20"/>
    </PivotItem>
</Pivot>
```

---

### Задание 61: Canvas для рисования и позиционирования

**Описание:** Используйте Canvas для произвольного позиционирования элементов.

**XAML:**
```xaml
<Canvas Background="LightGray" Width="400" Height="300">
    <Ellipse Canvas.Left="50" 
             Canvas.Top="50" 
             Width="100" 
             Height="100" 
             Fill="Red"/>
    <Rectangle Canvas.Left="200" 
               Canvas.Top="100" 
               Width="100" 
               Height="100" 
               Fill="Blue"/>
</Canvas>
```

---

### Задание 62: Media элементы (Audio/Video)

**Описание:** Создайте MediaElement для воспроизведения видео.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <MediaElement x:Name="VideoPlayer"
                  Source="ms-appx:///Assets/sample.mp4"
                  Height="300"
                  Width="400"/>
    <StackPanel Orientation="Horizontal" Spacing="10">
        <Button Content="Воспроизвести" Click="Play_Click"/>
        <Button Content="Пауза" Click="Pause_Click"/>
        <Button Content="Остановить" Click="Stop_Click"/>
    </StackPanel>
</StackPanel>
```

**C#:**
```csharp
private void Play_Click(object sender, RoutedEventArgs e)
{
    VideoPlayer.Play();
}

private void Pause_Click(object sender, RoutedEventArgs e)
{
    VideoPlayer.Pause();
}

private void Stop_Click(object sender, RoutedEventArgs e)
{
    VideoPlayer.Stop();
}
```

---

### Задание 63: Image и ImageBrush

**Описание:** Загрузите и отобразите изображение.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10">
    <Image Source="ms-appx:///Assets/sample.jpg" 
           Width="300" 
           Height="200"
           Stretch="UniformToFill"/>
    <Rectangle Width="300" 
               Height="200">
        <Rectangle.Fill>
            <ImageBrush ImageSource="ms-appx:///Assets/sample.jpg"/>
        </Rectangle.Fill>
    </Rectangle>
</StackPanel>
```

---

### Задание 64: Shape элементы (Ellipse, Rectangle, Polygon)

**Описание:** Создайте различные фигуры.

**XAML:**
```xaml
<StackPanel Padding="20" Spacing="10" Orientation="Horizontal">
    <Ellipse Fill="Red" Width="100" Height="100"/>
    <Rectangle Fill="Blue" Width="100" Height="100"/>
    <Polygon Points="50,0 100,50 50,100 0,50" 
             Fill="Green" 
             Width="100" 
             Height="100"/>
</StackPanel>
```

---

### Задание 65: Gradient и Effects

**Описание:** Создайте элемент с градиентной заливкой.

**XAML:**
```xaml
<Rectangle Width="300" Height="200">
    <Rectangle.Fill>
        <LinearGradientBrush StartPoint="0,0" EndPoint="1,1">
            <GradientStop Offset="0" Color="Red"/>
            <GradientStop Offset="0.5" Color="Yellow"/>
            <GradientStop Offset="1" Color="Blue"/>
        </LinearGradientBrush>
    </Rectangle.Fill>
</Rectangle>
```

---

### Задание 66: Transform для трансформации элементов

**Описание:** Примените трансформацию к элементу.

**XAML:**
```xaml
<Button Content="Нажми" 
        Width="100" 
        Height="50"
        RenderTransformOrigin="0.5,0.5">
    <Button.RenderTransform>
        <RotateTransform Angle="45"/>
    </Button.RenderTransform>
</Button>
```

---

### Задание 67: Диспетчеризация асинхронного кода

**Описание:** Используйте Dispatcher для обновления UI из фонового потока.

**C#:**
```csharp
private async void LoadDataFromBackground()
{
    await Task.Run(async () =>
    {
        var data = await FetchDataAsync();

        await Dispatcher.RunAsync(CoreDispatcherPriority.Normal, () =>
        {
            ResultTextBlock.Text = data;
        });
    });
}
```

---

### Задание 68: Свойства XAML Attached Properties

**Описание:** Создайте прикрепленное свойство.

**C#:**
```csharp
public static class CustomProperties
{
    public static string GetCustomLabel(DependencyObject obj)
    {
        return (string)obj.GetValue(CustomLabelProperty);
    }

    public static void SetCustomLabel(DependencyObject obj, string value)
    {
        obj.SetValue(CustomLabelProperty, value);
    }

    public static readonly DependencyProperty CustomLabelProperty =
        DependencyProperty.RegisterAttached(
            "CustomLabel",
            typeof(string),
            typeof(CustomProperties),
            new PropertyMetadata(null));
}
```

**XAML:**
```xaml
<TextBlock local:CustomProperties.CustomLabel="Это пользовательское свойство"/>
```

---

### Задание 69: Использование Storyboard для сложных анимаций

**Описание:** Создайте Storyboard с несколькими анимациями.

**XAML:**
```xaml
<StackPanel>
    <Rectangle x:Name="AnimatedRectangle" 
               Fill="Blue" 
               Width="100" 
               Height="100"/>
    <Button Content="Анимировать" Click="Animate_Click"/>

    <Storyboard x:Name="MyStoryboard">
        <DoubleAnimation Storyboard.TargetName="AnimatedRectangle"
                         Storyboard.TargetProperty="(Canvas.Left)"
                         From="0"
                         To="300"
                         Duration="0:0:2"/>
        <DoubleAnimation Storyboard.TargetName="AnimatedRectangle"
                         Storyboard.TargetProperty="(Canvas.Top)"
                         From="0"
                         To="200"
                         Duration="0:0:2"/>
    </Storyboard>
</StackPanel>
```

**C#:**
```csharp
private void Animate_Click(object sender, RoutedEventArgs e)
{
    MyStoryboard.Begin();
}
```

---

### Задание 70: Использование VisualStates для управления состояниями

**Описание:** Создайте VisualStates для разных состояний элемента.

**XAML:**
```xaml
<StackPanel>
    <VisualStateManager.VisualStateGroups>
        <VisualStateGroup x:Name="CommonStates">
            <VisualState x:Name="Normal">
                <Storyboard>
                    <DoubleAnimation Storyboard.TargetName="rect"
                                     Storyboard.TargetProperty="Opacity"
                                     To="1"
                                     Duration="0:0:0.3"/>
                </Storyboard>
            </VisualState>
            <VisualState x:Name="Pressed">
                <Storyboard>
                    <DoubleAnimation Storyboard.TargetName="rect"
                                     Storyboard.TargetProperty="Opacity"
                                     To="0.5"
                                     Duration="0:0:0.3"/>
                </Storyboard>
            </VisualState>
        </VisualStateGroup>
    </VisualStateManager.VisualStateGroups>

    <Rectangle x:Name="rect" Fill="Blue" Width="100" Height="100"/>
</StackPanel>
```

---

### Задание 71: Использование ThemeResources

**Описание:** Используйте системные ресурсы темы.

**XAML:**
```xaml
<TextBlock Text="Текст с системным цветом"
           Foreground="{ThemeResource ApplicationForeground}"
           Background="{ThemeResource ApplicationPageBackgroundThemeBrush}"/>
```

---

### Задание 72: Создание пользовательской ControlTemplate

**Описание:** Создайте пользовательский шаблон для комбинированного элемента.

**XAML:**
```xaml
<ControlTemplate x:Key="CustomButtonTemplate" TargetType="Button">
    <Grid>
        <VisualStateManager.VisualStateGroups>
            <VisualStateGroup x:Name="CommonStates">
                <VisualState x:Name="Normal"/>
                <VisualState x:Name="PointerOver">
                    <Storyboard>
                        <ColorAnimation Storyboard.TargetName="bg"
                                        Storyboard.TargetProperty="(Rectangle.Fill).(SolidColorBrush.Color)"
                                        To="LightBlue"
                                        Duration="0:0:0.2"/>
                    </Storyboard>
                </VisualState>
            </VisualStateGroup>
        </VisualStateManager.VisualStateGroups>

        <Rectangle x:Name="bg" Fill="Blue" CornerRadius="5"/>
        <ContentPresenter Content="{TemplateBinding Content}"
                          HorizontalAlignment="Center"
                          VerticalAlignment="Center"/>
    </Grid>
</ControlTemplate>

<Button Content="Пользовательская кнопка"
        Template="{StaticResource CustomButtonTemplate}"/>
```

---

### Задание 73: Использование RelativePanel для сложного макета

**Описание:** Создайте сложный макет с RelativePanel.

**XAML:**
```xaml
<RelativePanel Padding="20">
    <Image x:Name="ProfilePicture"
           Source="ms-appx:///Assets/profile.jpg"
           Width="100"
           Height="100"/>

    <TextBlock x:Name="Name"
               Text="John Doe"
               FontSize="24"
               FontWeight="Bold"
               RelativePanel.RightOf="ProfilePicture"
               RelativePanel.AlignVerticalCenterWith="ProfilePicture"
               Margin="20,0,0,0"/>

    <TextBlock x:Name="Email"
               Text="john@example.com"
               RelativePanel.Below="Name"
               Margin="0,10,0,0"/>

    <Button Content="Редактировать"
            RelativePanel.Below="ProfilePicture"
            Margin="0,20,0,0"/>
</RelativePanel>
```

---

### Задание 74: Использование AppBarToggleButton

**Описание:** Создайте переключаемую кнопку в CommandBar.

**XAML:**
```xaml
<CommandBar>
    <AppBarToggleButton Icon="Like" 
                        Label="Нравится" 
                        Checked="LikeButton_Checked"
                        Unchecked="LikeButton_Unchecked"/>
</CommandBar>
```

**C#:**
```csharp
private void LikeButton_Checked(object sender, RoutedEventArgs e)
{
    StatusTextBlock.Text = "Вам нравится!";
}

private void LikeButton_Unchecked(object sender, RoutedEventArgs e)
{
    StatusTextBlock.Text = "Вам больше не нравится";
}
```

---

### Задание 75: Использование Border для стилизации

**Описание:** Создайте красиво оформленный контейнер с Border.

**XAML:**
```xaml
<Border BorderBrush="Blue"
        BorderThickness="2"
        CornerRadius="8"
        Padding="20"
        Background="LightBlue">
    <StackPanel Spacing="10">
        <TextBlock Text="Заголовок" FontSize="20" FontWeight="Bold"/>
        <TextBlock Text="Содержимое контейнера" TextWrapping="Wrap"/>
    </StackPanel>
</Border>
```

---

### Задание 76-100: Проектные сценарии

Для заданий 76-100, предлагаются проектные сценарии, требующие применения нескольких элементов управления одновременно:

**Задание 76: Приложение "Список дел"**
- ListView для отображения задач
- TextBox для ввода новой задачи
- Button для добавления задачи
- Checkbox для отметки завершенной задачи
- StackPanel для макета

**Задание 77: Приложение "Калькулятор"**
- TextBox для отображения результата
- Grid для организации кнопок (0-9, +, -, *, /)
- Button для кнопок операций
- ObservableCollection для истории

**Задание 78: Форма регистрации**
- TextBox для имени, email
- PasswordBox для пароля
- ComboBox для выбора страны
- CheckBox для согласия с условиями
- Button для отправки
- Валидация данных

**Задание 79: Приложение "Погода"**
- ListView для списка городов
- TextBlock для температуры и описания
- Image для иконки погоды
- Button для обновления
- ProgressRing для загрузки

**Задание 80: Медиаплеер**
- MediaElement для видео/аудио
- Slider для текущего времени
- Button для управления (play, pause, stop)
- TextBlock для отображения времени
- Volume Slider

**Задание 81: Приложение "Галерея фотографий"**
- GridView для отображения фото
- Image для полного просмотра
- ComboBox для фильтров
- TextBox для поиска

**Задание 82: Приложение "Контакты"**
- ListView для списка контактов
- TextBox для поиска
- Button для добавления/удаления
- TextBlock для деталей контакта
- Border для карточек контактов

**Задание 83: Приложение "Заметки"**
- ListView для списка заметок
- TextBox для редактирования
- Button для сохранения
- DatePicker для даты создания
- ObservableCollection для управления

**Задание 84: Приложение "Опрос/Анкета"**
- RadioButton для выбора одного ответа
- CheckBox для множественного выбора
- TextBox для открытых вопросов
- Button для отправки
- ProgressBar для прогресса

**Задание 85: Приложение "Настройки"**
- ToggleSwitch для включения/отключения
- Slider для численных параметров
- ComboBox для выбора параметров
- Button для сохранения
- ContentDialog для подтверждения

**Задание 86: Приложение "Чат"**
- ListView для сообщений
- TextBox для ввода
- Button для отправки
- TextBlock для информации о пользователе
- ScrollViewer для прокрутки

**Задание 87: Приложение "Задачник"**
- NavigationView для навигации
- ListView для списка задач по категориям
- TextBox для поиска
- Button для действий
- ObservableCollection для данных

**Задание 88: Приложение "Расписание"**
- Grid для дней недели
- TextBlock для времени события
- Button для добавления события
- DatePicker для выбора даты
- TimePicker для выбора времени

**Задание 89: Приложение "Бюджет"**
- ListView для категорий расходов
- NumberBox для суммы
- ComboBox для категории
- ProgressBar для процента от бюджета
- TextBlock для статистики

**Задание 90: Приложение "Книга"**
- TextBlock для текста книги
- ScrollViewer для прокрутки
- Slider для размера шрифта
- ToggleSwitch для темного режима
- Button для навигации между главами

**Задание 91: Приложение "Опубликованные работы"**
- GridView для карточек работ
- Image для превью
- TextBlock для заголовка и описания
- Button для просмотра деталей
- ComboBox для фильтрации

**Задание 92: Приложение "Мессенджер"**
- ListView для контактов
- TextBox для ввода сообщения
- Button для отправки
- TextBlock для текста сообщения
- TimePicker для времени отправки

**Задание 93: Приложение "Магазин"**
- GridView для товаров
- Image для фото товара
- TextBlock для цены
- NumberBox для количества
- Button для добавления в корзину

**Задание 94: Приложение "Карты"**
- ComboBox для выбора маршрута
- TextBlock для информации о расстоянии
- Button для начала маршрута
- ProgressRing для загрузки
- Slider для масштаба

**Задание 95: Приложение "Новости"**
- ListView для списка новостей
- Image для изображения новости
- TextBlock для заголовка и содержимого
- Button для полного прочтения
- ComboBox для категорий

**Задание 96: Приложение "Калькулятор кредита"**
- TextBox для суммы кредита
- Slider для процентной ставки
- NumberBox для срока
- TextBlock для расчета
- Button для расчета

**Задание 97: Приложение "Таймер"**
- TextBlock для отображения времени
- NumberBox для установки времени
- Button для start/pause/stop
- ProgressRing для визуализации
- Slider для скорости

**Задание 98: Приложение "Угадай число"**
- TextBox для ввода числа
- Button для проверки
- TextBlock для подсказок
- ProgressBar для количества попыток
- Button для новой игры

**Задание 99: Приложение "Тесты/Квиз"**
- TextBlock для вопроса
- RadioButton для вариантов ответов
- Button для следующего вопроса
- ProgressBar для прогресса
- TextBlock для результата

**Задание 100: Приложение "Социальная сеть" (Микро версия)**
- ListView для ленты постов
- TextBox для создания поста
- Button для публикации
- Image для аватара
- TextBlock для информации профиля
- StackPanel для макета
- Border для оформления карточек постов

---

## Заключение

Этот набор из 100+ заданий покрывает основные и продвинутые техники работы с элементами управления UWP. Каждое задание строится на знаниях из предыдущих, создавая прогрессивную программу обучения.

### Рекомендации для обучения:

1. **Начните с заданий 1-25**: Овладейте базовыми элементами управления
2. **Переходите к заданиям 26-60**: Изучите навигацию, события и привязку данных
3. **Выполните задания 61-75**: Освойте продвинутые техники и анимации
4. **Реализуйте проектные сценарии 76-100**: Практикуйтесь на реальных приложениях

### Дополнительные ресурсы:

- [Microsoft Docs - UWP Controls](https://learn.microsoft.com/en-us/windows/apps/design/controls/)
- [XAML Documentation](https://learn.microsoft.com/en-us/uwp/api/windows.ui.xaml/)
- [WinUI 3 Gallery](https://github.com/microsoft/WinUI-Gallery)

### Советы:

- Экспериментируйте с кодом
- Создавайте собственные проекты
- Изучайте документацию Microsoft
- Попробуйте комбинировать разные элементы
- Обратите внимание на лучшие практики UX/UI

**Успехов в обучении!**

---

*Документ создан как учебный материал для изучения элементов управления UWP*
