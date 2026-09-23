ffc script Hokkubokku
{
	void run(int enemyID)
	{
		npc ghost = Ghost_InitAutoGhost(this, enemyID);
		
		if (Rand(1, 2) == 1)
		{
			Ghost_Vx = ghost->Step * 0.01;
		}
		else
		{
			Ghost_Vx = -1 * ghost->Step * 0.01;
		}
		
		if (Rand(1, 2) == 1)
		{
			Ghost_Vy = ghost->Step * 0.01;
		}
		else
		{
			Ghost_Vy = -1 * ghost->Step * 0.01;
		}
		int Data = Ghost_Data;
		Ghost_Jump = 0.75;
		Ghost_Z = 1;
		int savevx = 0;
		int savevy = 0;
		int jumpcounter = 0;
		int SegZ[3];
		npc Segment[3];
		int SegDist = 8;
		int Segments = 3;
		Ghost_SetFlag(GHF_FAKE_Z);
		while (true)
		{
			if (Ghost_Z > 0)
			{
				if (Ghost_Vx == 0)
				{
					if (savevx != 0) Ghost_Vx = savevx;
					else
					{
						if (Rand(1, 2) == 1)
						{
							Ghost_Vx = ghost->Step * 0.01;
						}
						else
						{
							Ghost_Vx = -1 * ghost->Step * 0.01;
						}
					}
				}
				if (Ghost_Vy == 0)
				{
					if (savevy != 0) Ghost_Vy = savevy;
					else
					{
						if (Rand(1, 2) == 1)
						{
							Ghost_Vy = ghost->Step * 0.01;
						}
						else
						{
							Ghost_Vy = -1 * ghost->Step * 0.01;
						}
					}
				}
				SegDist = 8;
				jumpcounter = 0;
				// Change X velocity when bouncing on vertical surface.
				if (!Ghost_CanMove(DIR_LEFT, ghost->Step * 0.01, 4) && Ghost_Vx < 0)
				{
					Ghost_Vx = ghost->Step * 0.01;
				}
				if (!Ghost_CanMove(DIR_RIGHT, ghost->Step * 0.01, 4) && Ghost_Vx > 0)
				{
					Ghost_Vx = -1 * ghost->Step * 0.01;
				}
				
				// Change Y velocity when bouncing on horizontal surface.
				if (!Ghost_CanMove(DIR_UP, ghost->Step * 0.01, 4) && Ghost_Vy < 0)
				{
					Ghost_Vy = ghost->Step * 0.01;
				}
				if (!Ghost_CanMove(DIR_DOWN, ghost->Step * 0.01, 4) && Ghost_Vy > 0)
				{
					Ghost_Vy = -1 * ghost->Step * 0.01;
				}
			}
			else
			{
				SegDist = 3 + Round(Abs(jumpcounter - 10) / 2);
				if (Ghost_Vx != 0)
				{
					savevx = Ghost_Vx;
					Ghost_Vx = 0;
				}
				if (Ghost_Vy != 0)
				{
					savevy = Ghost_Vy;
					Ghost_Vy = 0;
				}
				jumpcounter++;
				
				if (jumpcounter >= 20) Ghost_Jump = 1;
			}
			
			Segments = HokkuWait(this, ghost, SegDist, Segments, Segment, Data);
		}
	}
	int HokkuWait(ffc this, npc ghost, int SegDist, int Segments, npc Segment, int Data)
	{
		if (Ghost_GotHit() && Segments > 0)
		{
			Segments--;
			Segment[Segments] = Screen->CreateNPC(ghost->Attributes[0]);
			Segment[Segments]->X = Ghost_X;
			Segment[Segments]->Y = Ghost_Y - Ghost_Z;
		}
		if (Ghost_Z > 0)
		{
			if (Segments > 0)
			{
				Ghost_Data = Data + 3;
			}
			else
			{
				Ghost_Data = Data + 1;
			}
			if (Segments == 3)
			{
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 1), Data + 3, Ghost_CSet, 128);
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 2), Data + 3, Ghost_CSet, 128);
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 3), Data + 1, Ghost_CSet, 128);
			}
			if (Segments == 2)
			{
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 1), Data + 3, Ghost_CSet, 128);
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 2), Data + 1, Ghost_CSet, 128);
			}
			if (Segments == 1)
			{
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 1), Data + 1, Ghost_CSet, 128);
			}
			if(GH_SHADOW_TRANSLUCENT>0) Screen->DrawTile(2, Ghost_X, Ghost_Y, GH_SHADOW_TILE+__ghzhData[__GHI_SHADOW_FRAME], 1, 1, GH_SHADOW_CSET, -1, -1, 0, 0, 0, 0, true, OP_TRANS);
			else Screen->DrawTile(2, Ghost_X, Ghost_Y, GH_SHADOW_TILE+__ghzhData[__GHI_SHADOW_FRAME], 1, 1, GH_SHADOW_CSET, -1, -1, 0, 0, 0, 0, true, OP_OPAQUE);
		}
		else
		{
			if (Segments > 0)
			{
				Ghost_Data = Data + 2;
			}
			else
			{
				Ghost_Data = Data;
			}
			if (Segments == 3)
			{
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 1), Data + 2, Ghost_CSet, 128);
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 2), Data + 2, Ghost_CSet, 128);
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 3), Data, Ghost_CSet, 128);
			}
			if (Segments == 2)
			{
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 1), Data + 2, Ghost_CSet, 128);
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 2), Data, Ghost_CSet, 128);
			}
			if (Segments == 1)
			{
				Screen->FastCombo(3, this->X + Ghost_Vx, this->Y + Ghost_Vy - (SegDist * 1), Data, Ghost_CSet, 128);
			}
		}
		if (!Ghost_Waitframe(this, ghost, true, true))
		{
			if (Segment[0]->isValid())
			{
				Segment[0]->HP = 0;
				Segment[0]->X = -32;
				Segment[0]->Y = -32;
			}
			if (Segment[1]->isValid())
			{
				Segment[1]->HP = 0;
				Segment[1]->X = -32;
				Segment[1]->Y = -32;
			}
			if (Segment[2]->isValid())
			{
				Segment[2]->HP = 0;
				Segment[2]->X = -32;
				Segment[2]->Y = -32;
			}
			Ghost_HP = 0;
		}
		return Segments;
	}
}