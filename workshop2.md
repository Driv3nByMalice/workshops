# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил:
- Копысов Андрей Евгеньевич
- РИ-332901
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | ? |
| Задание 2 | * | ? |
| Задание 3 | * | ? |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
Научиться передавать в Unity данные из Google Sheets с помощью Python. Также научиться анализировать игровые переменные, описывать их изменение и поведение

## Задание 1
### Выберите одну из игровых переменных в игре СПАСТИ РТФ: Выживание (HP, SP, игровая валюта, здоровье и т.д.), опишите её роль в игре, условия изменения / появления и диапазон допустимых значений. Постройте схему экономической модели в игре и укажите место выбранного ресурса в ней.
Ход работы:
- Я выбрал переменную здоровье(hp), ее роль в игре - отображать, сколько здоровья осталось у персонажа, а так же ее величина влияет на условие конца игры.
  Изменение переменной:
  - если игрок получил урон, то величина здоровья уменьшается
  - если игрок во время прокачки выбрал соотвествующие навыки, то они восполняют здоровье
  Диапазон допустимых значений от 0 и до лимита, указанного в игре
- Схема экономической модели ресурса:
![375967234-06cc9fd8-b2e1-4c71-a48d-92e51eca96e1](https://github.com/user-attachments/assets/ab1614ea-8c05-4c7b-b9ba-d8d169a839db)

## Задание 2
### ### С помощью скрипта на языке Python заполните google-таблицу данными, описывающими выбранную игровую переменную в игре “СПАСТИ РТФ:Выживание”. Средствами google-sheets визуализируйте данные в google-таблице (постройте график / диаграмму и пр.) для наглядного представления выбранной игровой величины. Опишите характер изменения этой величины, опишите недостатки в реализации этой величины (например, в игре может произойти условие наступления эксплойта) и предложите до 3-х вариантов модификации условий работы с переменной, чтобы сделать игровой опыт лучше.
Ход работы:
- Для начала нужно определить как меняется выбранная мной игровая переменная:
Здоровье игрока меняется в зависимсоти от полученного им урона, следовательно, изменение этой переменной зависит от игрока и его навыка. Поскольку есть множество вариантов изменения этого параметра, я выбрал ситуацию, когда игрок периодически получает урон.
- Благодаря выбранной ситуации график изменения переменной выглядит, как прямая (В более сложных ситуациях график может иметь более сложное поведение):
<img width="1654" height="826" alt="image" src="https://github.com/user-attachments/assets/4a31cbae-e3c6-4e7b-9b4f-1b9291a5a3c1" />
Ссылка на таблицу: https://docs.google.com/spreadsheets/d/1IUh0FghrUFsQhuaDQMJUqyBqL8lvCbQQc-xJ8NylhNI/edit?gid=0#gid=0
- Из графика видно что величина меняется от 30 до 0, уменьшение величины происходит когда игрок получает урон (в данном примере -10), а увеличение, когда игрок использует навык вампиризм или заканчивает волну. Недостатков в реализации величины нет, так как она изменяется логично и просто.
- Заполнение таблицы было выполненно с помощью кода на Python:

```
import gspread
import numpy as np
gc = gspread.service_account(filename = 'unitydatasciense-455100-67858ab9ee7f.json') 
sh = gc.open("UnityWorkshop2")
current_hp = 30
i = 0
while current_hp >= 0:
    i += 1
    if i == 0:
        continue
    else:
        sh.sheet1.update_acell(('A' + str(i)), str(i))
        sh.sheet1.update_acell(('B' + str(i)), str(current_hp))
        print(current_hp)
        current_hp -= 10
```
- Поскольку, в игре СПАСТИ РТФ довольно мало взаимодействия с хп и мало условий его изменения, то можно дополнить функционал игры следющими способами:
    - Добавить предмет, который увеличивает текущее здоровье либо моментально, либо переодически.
    - Возможность расходовать текущее здоровье в замен на какой ресурс (например, патроны или валюту), в таком случае возможно придется добавить новые предметы/механики, чтобы не ломать логику игры.
    - Возможность увеличивать лимит здоровья на определенный промежуток времени, например, для битвы с боссом.


## Задание 3
### Настройте на сцене Unity воспроизведение звуковых файлов, описывающих динамику изменения выбранной переменной. Например, если выбрано здоровье главного персонажа вы можете выводить сообщения, связанные с его состоянием.
Ход работы:
- Для реализации данного задания я выделил правило, по которому описывается динамика изменения здоровья:
    - Если хп около лимита (hp >= 30), то воспроизводится звук "хороший"
    - Если хп около среднего значения (30 > hp >= 20), то воспроизводится звук "средний"
    - Если хп около минимума (hp < 20), то воспроизводится звук "плохой"
- Для отображения этой динамики в Unity я создал пустой GameObject с таким скриптом (референс с методички):
```C#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.Networking;
using SimpleJSON;

public class NewBehaviourScript : MonoBehaviour
{
    public AudioClip goodSpeak;
    public AudioClip normalSpeak;
    public AudioClip badSpeak;
    private AudioSource selectAudio;
    private Dictionary<string, float> dataSet = new Dictionary<string, float>();
    private bool statusStart = false;
    private int i = 1;
    void Start()
    {
        StartCoroutine(GoogleSheets());
    }
    void Update()
    {
        if (dataSet["Mon_" + i.ToString()] >= 30 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioGood());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
            Debug.Log("Проигрывается звук 'Horosho'");
        }
        if (dataSet["Mon_" + i.ToString()] < 30 & dataSet["Mon_" + i.ToString()] >= 20 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioNormal());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
            Debug.Log("Проигрывается звук 'Sredne'");
        }
        if (dataSet["Mon_" + i.ToString()] < 20 & statusStart == false & i != dataSet.Count)
        {
            StartCoroutine(PlaySelectAudioBad());
            Debug.Log(dataSet["Mon_" + i.ToString()]);
            Debug.Log("Проигрывается звук 'Ploho'");
        }
    }

    IEnumerator GoogleSheets()
    {
        UnityWebRequest curentResp = UnityWebRequest.Get("https://sheets.googleapis.com/v4/spreadsheets/1-TBYwyDcrPz_f4pHD6Jv8I1gbH_UNFmD-HplJS98Nkk/values/Лист1?key=AIzaSyBFrX6sxQ8GY5gv57Az0AXnpU1rQKbjwJU");
        yield return curentResp.SendWebRequest();
        string rawResp = curentResp.downloadHandler.text;
        var rawJson = JSON.Parse(rawResp);
        foreach (var itemRawJson in rawJson["values"])
        {
            var parseJson = JSON.Parse(itemRawJson.ToString());
            var selectRow = parseJson[0].AsStringList;
            dataSet.Add(("Mon_" + selectRow[0]), float.Parse(selectRow[1]));
        }
    }
    IEnumerator PlaySelectAudioGood()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = goodSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioNormal()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = normalSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(3);
        statusStart = false;
        i++;
    }
    IEnumerator PlaySelectAudioBad()
    {
        statusStart = true;
        selectAudio = GetComponent<AudioSource>();
        selectAudio.clip = badSpeak;
        selectAudio.Play();
        yield return new WaitForSeconds(4);
        statusStart = false;
        i++;
    }
}
```
- Ниже в Unity наглядно показано изменение здоровья и то, что скрипт работает верно.
<img width="1498" height="846" alt="image" src="https://github.com/user-attachments/assets/286825dd-a017-45e5-a07d-7af64ad2bf60" />

## Выводы

В ходе работы я научился ананлизировать ресурсы определенной игры, визуализировать изменения и поведения определенного ресурса(хп), с помощью соотвествующих схем и ПО.

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
