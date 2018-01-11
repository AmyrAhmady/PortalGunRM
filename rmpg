#include <a_samp>
#include <streamer>

enum playerPortalGunStats
{
	bool:playerHasGun,
	playerPortalFirstObj,
	playerPortalFirstArea,
	playerPortalSecondObj,
	playerPortalSecondArea,
	bool:playerWantsSecond,
	playerHoldingGun,
	Float:playerPortalEx[2],
	Float:playerPortalInt[2]
}

new playerPortalGun[MAX_PLAYERS][playerPortalGunStats];

#define _ppg playerPortalGun[playerid]

stock GivePlayerPortalGun(playerid)
{
    GivePlayerWeapon(playerid , 24 , 1000);
    SetPlayerAttachedObject(playerid,0,19513,6,0.256000,0.045999,0.149000,-178.199981,0.000000,90.599952,1.257000,2.077998,2.857999 , 0xFFFFFFFF , 0xFFFFFFFF);
	SetPlayerAttachedObject(playerid,1,19946,6,0.228000,0.024000,0.111000,0.000000,0.000000,0.000000,0.003999,0.004000,0.000999 );
	SetPlayerAttachedObject(playerid,2,19513,6,-0.026000,0.009000,-0.009000,92.099990,87.600021,0.000000,1.086000,1.210000,3.265999 , 0xFFFFFFFF , 0xFFFFFFFF);
	_ppg[playerHasGun] = true;
	_ppg[playerHoldingGun] = true;
	return 1;
}

static GetPosFromView(playerid, Float:distance, &Float:x, &Float:y, &Float:z)
{
  new Float:cx,Float:cy,Float:cz,Float:fx,Float:fy,Float:fz;
  GetPlayerCameraPos(playerid, cx, cy, cz);
  GetPlayerCameraFrontVector(playerid, fx, fy, fz);
  x = fx * distance + cx;
  y = fy * distance + cy;
  z = fz * distance + cz;
}

static Float:GetDistanceBetweenPoints3D(Float:x1,Float:y1,Float:z1,Float:x2,Float:y2,Float:z2){
    return VectorSize(x1-x2,y1-y2,z1-z2);
}

stock GetXYInFrontOfPortal(objid , &Float:x, &Float:y, Float:distance)
{
	new Float:a1 , Float:z , Float:a;
	GetDynamicObjectRot(objid , x, y, a1);
	GetDynamicObjectPos(objid, x, y, z);
	a = a1+180;
	x += (distance * floatsin(-a, degrees));
	y += (distance * floatcos(-a, degrees));
}

public OnPlayerWeaponShot(playerid, weaponid, hittype, hitid, Float:fX, Float:fY, Float:fZ)
{
    
	new Float:x , Float:y , Float:z;
	new Float:x_vector,Float:y_vetor,Float:z_vector;
	GetPlayerPos(playerid , x ,y ,z);
	new Float:dist = GetDistanceBetweenPoints3D(x , y , z , fX , fY , fZ);
	if(_ppg[playerHoldingGun])
	{
		if(dist <= 25.0)
		{
		    if(!_ppg[playerWantsSecond])
		    {
		    	if(IsValidDynamicObject(_ppg[playerPortalFirstObj]))
				{
					DestroyDynamicObject(_ppg[playerPortalFirstObj]);
					DestroyDynamicArea(_ppg[playerPortalFirstArea]);
				}
	    		_ppg[playerPortalFirstObj] = CreateDynamicObject(18886 , fX ,fY ,fZ+0.5 , 0.0 , 0.0 , 0.0);
				SetDynamicObjectMaterial(_ppg[playerPortalFirstObj] , 0 , 16198 , "des_cen" , "des_scrub1" , 0xEE00ff40);
				SetDynamicObjectMaterial(_ppg[playerPortalFirstObj] , 1 , 16198 , "des_cen" , "des_scrub1" , 0xEE00ff40);
				SetDynamicObjectMaterial(_ppg[playerPortalFirstObj] , 2 , 16198 , "des_cen" , "des_scrub1" , 0xEE00ff40);
				GetPlayerCameraFrontVector(playerid, x_vector, y_vetor, z_vector);
				SetDynamicObjectRot(_ppg[playerPortalFirstObj], asin(z_vector+0.01)-90.0, 0.0, 360 - atan2(x_vector, y_vetor));
				_ppg[playerPortalFirstArea] = CreateDynamicCylinder( fX , fY , fZ+0.5-(3.75092/2) , fZ+0.5+(3.75092/2) , 1.8);
			} else
			{
				if(IsValidDynamicObject(_ppg[playerPortalSecondObj]))
				{
					DestroyDynamicObject(_ppg[playerPortalSecondObj]);
					DestroyDynamicArea(_ppg[playerPortalSecondArea]);
				}
	    		_ppg[playerPortalSecondObj] = CreateDynamicObject(18886 , fX ,fY ,fZ+0.5 , 0.0 , 0.0 , 0.0);
				SetDynamicObjectMaterial(_ppg[playerPortalSecondObj] , 0 , 16198 , "des_cen" , "des_scrub1" , 0xEE00bfff);
				SetDynamicObjectMaterial(_ppg[playerPortalSecondObj] , 1 , 16198 , "des_cen" , "des_scrub1" , 0xEE00bfff);
				SetDynamicObjectMaterial(_ppg[playerPortalSecondObj] , 2 , 16198 , "des_cen" , "des_scrub1" , 0xEE00bfff);
				GetPlayerCameraFrontVector(playerid, x_vector, y_vetor, z_vector);
				SetDynamicObjectRot(_ppg[playerPortalSecondObj], asin(z_vector+0.01)-90.0, 0.0, 360 - atan2(x_vector, y_vetor));
				_ppg[playerPortalSecondArea] = CreateDynamicCylinder( fX , fY , fZ+0.5-(3.75092/2) , fZ+0.5+(3.75092/2) , 1.8);
			}
		
		} else
		{
		    if(!_ppg[playerWantsSecond])
		    {
		    	if(IsValidDynamicObject(_ppg[playerPortalFirstObj]))
				{
					DestroyDynamicObject(_ppg[playerPortalFirstObj]);
					DestroyDynamicArea(_ppg[playerPortalFirstArea]);
				}
				GetPosFromView(playerid , 18.0 , x ,y , z);
				_ppg[playerPortalFirstObj] = CreateDynamicObject(18886 , x ,y ,z+1.2 , 0.0 , 0.0 , 0.0);
				SetDynamicObjectMaterial(_ppg[playerPortalFirstObj] , 0 , 16198 , "des_cen" , "des_scrub1" , 0xEE00ff40);
				SetDynamicObjectMaterial(_ppg[playerPortalFirstObj] , 1 , 16198 , "des_cen" , "des_scrub1" , 0xEE00ff40);
				SetDynamicObjectMaterial(_ppg[playerPortalFirstObj] , 2 , 16198 , "des_cen" , "des_scrub1" , 0xEE00ff40);
				GetPlayerCameraFrontVector(playerid, x_vector, y_vetor, z_vector);
				SetDynamicObjectRot(_ppg[playerPortalFirstObj], asin(z_vector+0.01)-90.0, 0.0, 360 - atan2(x_vector, y_vetor));
				_ppg[playerPortalFirstArea] = CreateDynamicCylinder( x , y , z+1.2-(3.75092/2) , z+1.2+(3.75092/2) , 1.8);
			} else
			{
			    if(IsValidDynamicObject(_ppg[playerPortalSecondObj]))
				{
					DestroyDynamicObject(_ppg[playerPortalSecondObj]);
					DestroyDynamicArea(_ppg[playerPortalSecondArea]);
				}
				GetPosFromView(playerid , 18.0 , x ,y , z);
				_ppg[playerPortalSecondObj] = CreateDynamicObject(18886 , x ,y ,z+1.2 , 0.0 , 0.0 , 0.0);
				SetDynamicObjectMaterial(_ppg[playerPortalSecondObj] , 0 , 16198 , "des_cen" , "des_scrub1" , 0xEE00bfff);
				SetDynamicObjectMaterial(_ppg[playerPortalSecondObj] , 1 , 16198 , "des_cen" , "des_scrub1" , 0xEE00bfff);
				SetDynamicObjectMaterial(_ppg[playerPortalSecondObj] , 2 , 16198 , "des_cen" , "des_scrub1" , 0xEE00bfff);
				GetPlayerCameraFrontVector(playerid, x_vector, y_vetor, z_vector);
				SetDynamicObjectRot(_ppg[playerPortalSecondObj], asin(z_vector+0.01)-90.0, 0.0, 360 - atan2(x_vector, y_vetor));
				_ppg[playerPortalSecondArea] = CreateDynamicCylinder( x , y , z+1.2-(3.75092/2) , z+1.2+(3.75092/2) , 1.8);
			}
    	}
    }
    return CallLocalFunction("ppg_OnPlayerWeaponShot", "iiiifff", playerid , weaponid, hittype, hitid, fX, fY, fZ);
}

#if defined _ALS_OnPlayerWeaponShot
	#undef OnPlayerWeaponShot
#else
	#define _ALS_OnPlayerWeaponShot
#endif
#define OnPlayerWeaponShot ppg_OnPlayerWeaponShot
forward ppg_OnPlayerWeaponShot(playerid , weaponid, hittype, hitid, Float:fX, Float:fY, Float:fZ);

public OnPlayerConnect(playerid)
{
    _ppg[playerHasGun]=false;
    _ppg[playerWantsSecond]=false;
    _ppg[playerHoldingGun] = false;
    
    return CallLocalFunction("ppg_OnPlayerConnect", "i", playerid);
}

#if defined _ALS_OnPlayerConnect
	#undef OnPlayerConnect
#else
	#define _ALS_OnPlayerConnect
#endif
#define OnPlayerConnect ppg_OnPlayerConnect
forward ppg_OnPlayerConnect(playerid);

public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
	if((newkeys & (KEY_WALK)) == (KEY_WALK))
	{
		_ppg[playerWantsSecond]=true;
	}
	if((oldkeys & KEY_WALK) && !(newkeys & KEY_WALK))
	{
	    _ppg[playerWantsSecond]=false;
	}
	return CallLocalFunction("ppg_OnPlayerKeyStateChange", "iii", playerid , newkeys , oldkeys);
}

#if defined _ALS_OnPlayerKeyStateChange
	#undef OnPlayerKeyStateChange
#else
	#define _ALS_OnPlayerKeyStateChange
#endif
#define OnPlayerKeyStateChange ppg_OnPlayerKeyStateChange
forward ppg_OnPlayerKeyStateChange(playerid , newkeys , oldkeys);

public OnPlayerUpdate(playerid)
{
    new iCurWeap = GetPlayerWeapon(playerid); 
    if(iCurWeap != GetPVarInt(playerid, "iCurrentWeapon")) 
    {
        _ppg_OnPlayerChangeWeapon(playerid, GetPVarInt(playerid, "iCurrentWeapon"), iCurWeap);
        SetPVarInt(playerid, "iCurrentWeapon", iCurWeap);
    }
    return CallLocalFunction("ppg_OnPlayerUpdate", "i", playerid);
}

#if defined _ALS_OnPlayerUpdate
	#undef OnPlayerUpdate
#else
	#define _ALS_OnPlayerUpdate
#endif
#define OnPlayerUpdate ppg_OnPlayerUpdate
forward ppg_OnPlayerUpdate(playerid);

public OnPlayerEnterDynamicArea(playerid , areaid)
{
	if(areaid == _ppg[playerPortalSecondArea])
	{
	    if(IsValidDynamicArea(_ppg[playerPortalFirstArea]))
	    {
			new Float:rx , Float:ry , Float:rz,
			    Float:x  , Float:y  , Float:z ;
			GetDynamicObjectRot(_ppg[playerPortalFirstObj]  , rx , ry , rz);
			GetDynamicObjectPos(_ppg[playerPortalFirstObj]  , x  , y  , z );
			GetXYInFrontOfPortal(_ppg[playerPortalFirstObj] , x  , y  , 2.4);
			SetPlayerPos(playerid , x , y ,z);
			SetPlayerFacingAngle(playerid , rz+180.0);
		}
	}
	if(areaid == _ppg[playerPortalFirstArea])
	{
	    if(IsValidDynamicArea(_ppg[playerPortalSecondArea]))
	    {
			new Float:rx , Float:ry , Float:rz,
			    Float:x  , Float:y  , Float:z ;
			GetDynamicObjectRot(_ppg[playerPortalSecondObj] , rx , ry , rz);
			GetDynamicObjectPos(_ppg[playerPortalSecondObj] , x  , y  , z );
			GetXYInFrontOfPortal(_ppg[playerPortalSecondObj] , x  , y  , 2.4);
			SetPlayerPos(playerid , x , y ,z);
			SetPlayerFacingAngle(playerid , rz+180.0);
		}
	}
	return CallLocalFunction("ppg_OnPlayerEnterDynamicArea", "ii", playerid , areaid);
}

#if defined _ALS_OnPlayerEnterDynamicArea
	#undef OnPlayerEnterDynamicArea
#else
	#define _ALS_OnPlayerEnterDynamicArea
#endif
#define OnPlayerEnterDynamicArea ppg_OnPlayerEnterDynamicArea
forward ppg_OnPlayerEnterDynamicArea(playerid, areaid);

stock _ppg_OnPlayerChangeWeapon(playerid, oldweapon, newweapon)
{
    if(oldweapon == 24)
    {
        if(_ppg[playerHasGun])
        {
            RemovePlayerAttachedObject(playerid , 0);
            RemovePlayerAttachedObject(playerid , 1);
            RemovePlayerAttachedObject(playerid , 2);
            _ppg[playerHoldingGun] = false;
        }
	}
	if(newweapon == 24)
    {
        if(_ppg[playerHasGun])
        {
            SetPlayerAttachedObject(playerid,0,19513,6,0.256000,0.045999,0.149000,-178.199981,0.000000,90.599952,1.257000,2.077998,2.857999 , 0xFFFFFFFF , 0xFFFFFFFF);
			SetPlayerAttachedObject(playerid,1,19946,6,0.228000,0.024000,0.111000,0.000000,0.000000,0.000000,0.003999,0.004000,0.000999 );
			SetPlayerAttachedObject(playerid,2,19513,6,-0.026000,0.009000,-0.009000,92.099990,87.600021,0.000000,1.086000,1.210000,3.265999 , 0xFFFFFFFF , 0xFFFFFFFF);
			_ppg[playerHoldingGun] = true;
        }
	}
}
