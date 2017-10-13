using System;
using Microsoft.Xna.Framework;
using Microsoft.Xna.Framework.Graphics;
using Microsoft.Xna.Framework.Input;

class TetrisGrid
{
    int Timer = 0, D = 0, S = 0;
    bool[,] grid, square;

    public TetrisGrid(Texture2D b)
    {
        grid = new bool[12, 20];
        grid[11,19] = true;

        square = new bool[4, 4]
        {
            { false,false,false,false },
            { false,false,false,false },
            { false,true,true,false },
            { true,true,false,false }
        };

       /* square[0, 0] = true;
        square[0, 1] = true;
        square[0, 2] = false;
        square[0, 3] = false;
        square[1, 0] = false;
        square[1, 1] = true;
        square[1, 2] = true;
        square[1, 3] = false;
        square[2, 0] = false;
        square[2, 1] = false;
        square[2, 2] = false;
        square[2, 3] = false;
        square[3, 0] = false;
        square[3, 1] = false;
        square[3, 2] = false;
        square[3, 3] = false; */

        gridblock = b;
        position = Vector2.Zero;
        this.Clear();
    }

    Texture2D gridblock;

    Vector2 position;

    public void HandleInput(GameTime gameTime, InputHelper inputHelper)
    {
    }

    public void Update(GameTime gameTime)
    {
        KeyboardState CurrentKBState = Keyboard.GetState();

        Timer += gameTime.ElapsedGameTime.Milliseconds;
        if (Timer >= 600 && D < Height-3)
        {
            Timer -= 600;
            D++;
        } 
        if (CurrentKBState.IsKeyDown(Keys.Right) && D < Height-3 && S <= 7)
        {
            S++;
        }
        if (CurrentKBState.IsKeyDown(Keys.Left) && D < Height-3 && S >= -1)
        {
            S--;
        }
        if (CurrentKBState.IsKeyDown(Keys.Down) && D < Height - 3)
        {
            D++;
        }
        if (CurrentKBState.IsKeyDown(Keys.Enter) && D < Height - 3)
        {
            D = Height - 3;
        }

    }

    public int Width
    {
        get { return 12; }
    }

    public int Height
    {
        get { return 20; }
    }

    public void Clear()
    {
    }

    public void array()
    {
    } 

    public void Drawgrid(GameTime gameTime, SpriteBatch s)
    {
        for (int y = 0; y < Height; y++)
            for (int x = 0; x < Width; x++)
            {
                if (x >= S && x < S + 4 && y >= D && y < D + 4)
                {
                    if (square[x-S, y-D] == true)
                    {
                        s.Draw(gridblock, new Vector2(x * gridblock.Width, y * gridblock.Height), Color.Blue);
                    }
                    else
                    {
                        s.Draw(gridblock, new Vector2(gridblock.Width * x, gridblock.Height * y), Color.White);
                    }
                }
                else
                {
                    s.Draw(gridblock, new Vector2(gridblock.Width * x, gridblock.Height * y), Color.White);
                }
            }
    }

    public void Drawblock(GameTime gameTime, SpriteBatch s)
    {
    }
}

