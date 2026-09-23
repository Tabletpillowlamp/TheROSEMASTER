ffc script AntiFairy
{
	void run(int enemyID)
	{
		npc ghost = Ghost_InitAutoGhost(this, enemyID);
		int Num = ghost->Attributes[0];
		if (Num == 0) Num = -1;
		if (ghost->Attributes[1] > 0)
		{
			int dir = AngleDir8(Angle(Link->X, Link->Y, Ghost_X, Ghost_Y));
			if (dir == DIR_UP || dir == DIR_RIGHTUP || dir == DIR_LEFTUP) Ghost_Vy = -1 * ghost->Step * 0.01;
			else if (dir == DIR_DOWN || dir == DIR_RIGHTDOWN || dir == DIR_LEFTDOWN) Ghost_Vy = ghost->Step * 0.01;
			
			if (dir == DIR_LEFT || dir == DIR_LEFTDOWN || dir == DIR_LEFTUP) Ghost_Vx = -1 * ghost->Step * 0.01;
			else if (dir == DIR_RIGHT || dir == DIR_RIGHTDOWN || dir == DIR_RIGHTUP) Ghost_Vx = ghost->Step * 0.01;
			
			if (dir == DIR_UP || dir == DIR_DOWN) Ghost_Vy *= 4;
			else if (dir == DIR_LEFT || dir == DIR_RIGHT) Ghost_Vx *= 4;
		}
		else
		{
			if (Rand(2) == 0)
			{
				Ghost_Vx = ghost->Step * 0.01;
			}
			else
			{
				Ghost_Vx = -ghost->Step * 0.01;
			}
			
			if (Rand(2) == 0)
			{
				Ghost_Vy = ghost->Step * 0.01;
			}
			else
			{
				Ghost_Vy = -ghost->Step * 0.01;
			}
		}
		
		while (true)
		{
			if (!Ghost_CanMove(DIR_LEFT, ghost->Step * 0.01, 4) && Ghost_Vx < 0)
			{
				Ghost_Vx = -Ghost_Vx;
				if (Num > 0 && Num != -1) Num--;
			}
			else if (!Ghost_CanMove(DIR_RIGHT, ghost->Step * 0.01, 4) && Ghost_Vx > 0)
			{
				Ghost_Vx = -Ghost_Vx;
				if (Num > 0 && Num != -1) Num--;
			}
			
			// Change Y velocity when bouncing on horizontal surface.
			if (!Ghost_CanMove(DIR_UP, ghost->Step * 0.01, 4) && Ghost_Vy < 0)
			{
				Ghost_Vy = -Ghost_Vy;
				if (Num > 0 && Num != -1) Num--;
			}
			else if (!Ghost_CanMove(DIR_DOWN, ghost->Step * 0.01, 4) && Ghost_Vy > 0)
			{
				Ghost_Vy = -Ghost_Vy;
				if (Num > 0 && Num != -1) Num--;
			}
			if (Num == 0) 
			{
				lweapon Death = Screen->CreateLWeapon(LW_SPARKLE);
				Death->UseSprite(109);
				Death->X = Ghost_X;
				Death->Y = Ghost_Y;
				Ghost_X = -32;
				Ghost_Y = -32;
				Ghost_HP = 0;
			}
			Ghost_Waitframe(this, ghost, true, true);
		}
	}
}