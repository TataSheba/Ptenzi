
#include "TXLib.h"

void MyClear (COLORREF color);

const int mainX = 570, mainY = 570;


//{============================================================================
//!  Проведи птичку к гнезду
//}============================================================================

int main()
    {
    txCreateWindow (mainX, mainY);
    txBegin();

    HDC TreeImg  = txLoadImage ("ptenzi.bmp");
    HDC MapImg   = txLoadImage ("ptenziMAP.bmp");
    HDC CrownImg = txLoadImage("CrownAlfa.bmp");

    //--- Стартовые Данные птички----
    int x = 450;
    int y = 450;
    int frameX = 4;
    int frameY = 2;
    int frameSizeX = txGetExtentX (CrownImg) / frameX;
    int frameSizeY = txGetExtentY (CrownImg) / frameY;
    int anim = 0;
    int oldX;
    int oldY;

//---- Главный цикл игры--------
    for (int t=0; !txGetAsyncKeyState (VK_ESCAPE); t++)
        {
        //---- Читерская карта------
        if (!txGetAsyncKeyState (VK_SCROLL))
            txBitBlt (txDC(),  0, 0, 0, 0, MapImg);

        //---- Дерево------
        if (!txGetAsyncKeyState (VK_CAPITAL))
            txBitBlt (txDC(),  0, 0, 0, 0, TreeImg);

        //------Рисовать летящую птичку. Управление - КУК------------
        oldX = x;
        oldY = y;
        if (txGetAsyncKeyState (VK_LEFT))
            x -= 10;
        if (txGetAsyncKeyState (VK_RIGHT))
            x += 10;
        if (txGetAsyncKeyState (VK_UP))
            y -= 10;
        if (txGetAsyncKeyState (VK_DOWN))
            y += 10;
        //if (txGetAsyncKeyState ('1')) anim = 0;
        //if (txGetAsyncKeyState ('2')) anim = 1;

            //--- рисование кадра с птичкой-----
        txAlphaBlend (txDC(), x, y,
                    frameSizeX, frameSizeY,
                    CrownImg,
                    (t%frameX)*frameSizeX, anim*frameSizeY);

        // --- проверка на разрешение по ЦВЕТУ пиксела ----

            COLORREF color = txGetPixel ((int)(x+frameSizeX)/2, (int)(y+frameSizeY)/2, MapImg);
            //$x(color);/// это верхняя треть рисунка птички

        //   зеленый - передвижение
        if (color == RGB ( 0, 255, 0))
            {
            oldX = x;
            oldY = y;
            }


         // красный - запрет
        if (color == RGB (255, 0, 0))
            {
            x = oldX;
            y = oldY;
            }

        // синий - победа
        if (color == RGB (0, 0, 255))
            {
            win = TRUE;
            }

        if (win) txMessageBox ("ПОБЕДА!!!!");

           txSleep(10);
        }

    txDeleteDC (CrownImg);
    txDeleteDC (TreeImg);
    txDeleteDC (MapImg);

    txEnd();

    return 0;
    }
